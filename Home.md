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
path includes Periodic Notes
sort by urgency
``` 
````

## MOC

````ad-flex
<div>

```dataview
table  WITHOUT ID file.link as FILE
from #moc
```
</div>

````


````ad-flex
<div>

### 最近编辑
```dataview
table WITHOUT ID file.link AS "标题",file.mtime as "时间"
from !"Templates" and !"Periodic Notes" and -#moc
sort file.mtime desc
limit 10
```
</div>

<div>

### 七天内创建的笔记
```dataview
table file.ctime as 创建时间
from !"Templates" and !"Periodic Notes" and -#moc
where date(today) - file.ctime <=dur(7 days)
sort file.ctime desc
limit 10
```
</div>
````
