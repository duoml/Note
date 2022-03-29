---
<%*
var fileDate = moment(tp.file.title);
// moment dates are mutable
let prevMonth = moment(fileDate).subtract(1, 'M').format('YYYY-MM');
let nextMonth = moment(fileDate).add(1, 'M').format('YYYY-MM');
let yearLink = fileDate.format('YYYY');
let quarterLink = fileDate.format('YYYY-[Q]Q');
let monthLink = fileDate.format('YYYY-MM');
-%>
tags: monthly_note <% monthLink %> <% quarterLink %> <% yearLink %>
---
<%*
// ❮❮ ⋮ 2021 › Q4 ⋮ ❯❯
// [[path/to/file|display_text]]
let navStr = `[[Periodic Notes/Monthly/${prevMonth}|❮❮]] ⋮ [[Periodic Notes/Yearly/${yearLink}|${yearLink}]] › [[Periodic Notes/Quarterly/${quarterLink}|${fileDate.format('[Q]Q')}]] ⋮ [[Periodic Notes/Monthly/${nextMonth}|❯❯]]`;
tR += navStr
%>

## Done this month
```tasks
done after <% moment(fileDate).subtract(1, "M").endOf("month").format('YYYY-MM-DD') %>
done before <% moment(fileDate).add(1, "M").startOf("month").format('YYYY-MM-DD') %>
sort by done reverse
```
