
inline时需要callee的一些信息, 依赖callee对应的JSFunction.

## 1. 通过ProfileTypeInfo传递JSFunction
	
`ProfilerStubBuilder::ProfileCall`原本在对应的slot放置一个`Method*`, 修改为放置一个`JSFunction*`
![[Pasted image 20240504092705.png]]

## 2. JITProfiler::ConvertCall完善
这一步主要是处理pgo采集的数据, 转换为PGOType
![[Pasted image 20240504093416.png]]

`PGOProfiler::DumpCall`也需要做一些修改, 以对应ProfileTypeInfo中的变化

## 3. 保存callee的JSFunction
![[Pasted image 20240504093954.png]]
将`JSFunction*`对应的MethodOffset->slotId的映射保存在`JitCompilationEnv`中, 这样后续优化可以从中获取callee对应的JSFunction在caller的ProfileTypeInfo中的slotId, 进而获取JSFunction*

## 4. inline优化的补全

### 1. BCInfo
inline需要callee对应的BCInfo, 而Ctx中只保存了当前caller的 
Caller的BCInfo在`BytecodeInfoCollector::ProcessMethod`中获取, 可以稍作修改以获取callee对应的BCInfo
![[Pasted image 20240504095738.png]]
inline时调用
![[Pasted image 20240504100011.png]]
### 2. 满足inline条件时获取callee的ProfileTypeInfo转换为PGOType
![[Pasted image 20240504100140.png]]
因为这里无法构造带JSHandle的profileTypeInfo, 将JITProfiler::ProfileBytecode的第一个参数修改为裸指针
![[Pasted image 20240504100413.png]]