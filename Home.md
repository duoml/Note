---
banner: "https://img.xjh.me/random_img.php?type=bg&ctype=nature&return=302"
cssclass: fullwidth,noyaml,noscroll,myhome
banner_x: 0.47216
---

## TODO
````ad-flex
title:
collapse: none
icon: list
```tasks
not done
path includes Daily Notes
sort by urgency
``` 
````

## MOC

````ad-flex
<div>

### 快速导航
</div>
````


````ad-flex
<div>

### 最近编辑
```dataview
table WITHOUT ID file.link AS "标题",file.mtime as "时间"
from !"模板" and !"kanban"
sort file.mtime desc
limit 5
```
</div>

<div>

### 三天内创建的笔记
```dataview
table file.ctime as 创建时间
from ""
where date(today) - file.ctime <=dur(3 days)
sort file.ctime desc
limit 5
```
</div>
````

