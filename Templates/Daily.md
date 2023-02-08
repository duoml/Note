---
<%*
var fileDate = moment(tp.file.title);
// moment dates are mutable
let prevDay = moment(fileDate).subtract(1, 'd').format('YYYY-MM-DD');
let nextDay = moment(fileDate).add(1, 'd').format('YYYY-MM-DD');
let yearLink = fileDate.format('YYYY');
let quarterLink = fileDate.format('YYYY-[Q]Q');
let monthLink = fileDate.format('YYYY-MM');
let weekLink = fileDate.format('gggg-[W]WW');
-%>
tags: daily_note <% weekLink %> <% monthLink %> <% quarterLink %> <% yearLink %>
weekday: <% fileDate.format("ddd") %>
---
<%*
// ❮❮ ⋮ 2021 › Q4 › 12 › W49 ⋮ ❯❯
// [[path/to/file|display_text]]
let navStr = `[[Periodic Notes/Daily/${prevDay}|❮❮]] ⋮ [[Periodic Notes/Yearly/${yearLink}|${yearLink}]] › [[Periodic Notes/Quarterly/${quarterLink}|${fileDate.format('[Q]Q')}]] › [[Periodic Notes/Monthly/${monthLink}|${fileDate.format('MM')}]] › [[Periodic Notes/Weekly/${weekLink}|${fileDate.format('[W]WW')}]] ⋮ [[Periodic Notes/Daily/${nextDay}|❯❯]]`;
tR += navStr
%>
## Daily Log

## Done today 
```tasks 
done on <% fileDate.format("YYYY-MM-DD") %>
``` 

