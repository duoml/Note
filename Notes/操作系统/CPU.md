# cpu调度

## linux 完全公平调度算法（CFS）

Completely Fair Scheduler，完全公平调度器，用于Linux系统中普通进程的调度

CFS采用了红黑树算法来管理所有的调度实体sched_entity，算法效率为O(log(n))。CFS跟踪调度实体sched_entity的虚拟运行时间vruntime，平等对待运行队列中的调度实体sched_entity，将执行时间少的调度实体sched_entity排列到红黑树的左边。

- 每个sched_latency周期内，根据各个任务的权重值，可以计算出运行时间runtime；
- 运行时间runtime可以转换成虚拟运行时间vruntime；
- 根据虚拟运行时间的大小，插入到CFS红黑树中，虚拟运行时间少的调度实体放置到左边；
- 在下一次任务调度的时候，选择虚拟运行时间少的调度实体来运行

所谓调度，就是按照某种调度的算法，从进程的就绪队列中选取进程分配CPU，主要是协调对CPU等的资源使用。进程调度的目标是最大限度利用CPU时间。

内核默认提供了5个调度器，Linux内核使用struct sched_class来对调度器进行抽象：

1. Stop调度器， stop_sched_class：优先级最高的调度类，可以抢占其他所有进程，不能被其他进程抢占；
2. Deadline调度器， dl_sched_class：使用红黑树，把进程按照绝对截止期限进行排序，选择最小进程进行调度运行；
3. RT调度器， rt_sched_class：实时调度器，为每个优先级维护一个队列；
4. CFS调度器， cfs_sched_class：完全公平调度器，采用完全公平调度算法，引入虚拟运行时间概念；
5. IDLE-Task调度器， idle_sched_class：空闲调度器，每个CPU都会有一个idle线程，当没有其他进程可以调度时，调度运行idle线程；

Linux内核提供了一些调度策略供用户程序来选择调度器，其中Stop调度器和IDLE-Task调度器，仅由内核使用，用户无法进行选择：

- SCHED_DEADLINE：限期进程调度策略，使task选择Deadline调度器来调度运行；
- SCHED_RR：实时进程调度策略，时间片轮转，进程用完时间片后加入优先级对应运行队列的尾部，把CPU让给同优先级的其他进程；
- SCHED_FIFO：实时进程调度策略，先进先出调度没有时间片，没有更高优先级的情况下，只能等待主动让出CPU；
- SCHED_NORMAL：普通进程调度策略，使task选择CFS调度器来调度运行；
- SCHED_BATCH：普通进程调度策略，批量处理，使task选择CFS调度器来调度运行；
- SCHED_IDLE：普通进程调度策略，使task以最低优先级选择CFS调度器来调度运行；
