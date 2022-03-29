---
<%*
var fileDate = moment(tp.file.title);
// moment dates are mutable
let prevWeek = moment(fileDate).subtract(1, 'w').format('gggg-[W]WW');
let nextWeek = moment(fileDate).add(1, 'w').format('gggg-[W]WW');
let yearLink = fileDate.format('YYYY');
let quarterLink = fileDate.format('YYYY-[Q]Q');
let monthLink = fileDate.format('YYYY-MM');
let weekLink = fileDate.format('gggg-[W]WW');
-%>
tags: weekly_note <% weekLink %> <% monthLink %> <% quarterLink %> <% yearLink %>
---
<%*
// ❮❮ ⋮ 2021 › Q4 › 12  ⋮ ❯❯
// [[path/to/file|display_text]]
let navStr = `[[Periodic Notes/Weekly/${prevWeek}|❮❮]] ⋮ [[Periodic Notes/Yearly/${yearLink}|${yearLink}]] › [[Periodic Notes/Quarterly/${quarterLink}|${fileDate.format('[Q]Q')}]] › [[Periodic Notes/Monthly/${monthLink}|${fileDate.format('MM')}]] ⋮ [[Periodic Notes/Weekly/${nextWeek}|❯❯]]`;
tR += navStr
%>


## Done this week
```tasks
done after <% moment(fileDate).subtract(1, "w").endOf("week").format('YYYY-MM-DD') %>
done before <% moment(fileDate).add(1, "w").startOf("week").format('YYYY-MM-DD') %>
sort by done reverse
```