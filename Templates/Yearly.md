---
<%*
var fileDate = moment(tp.file.title);
// moment dates are mutable
let prevYear = moment(fileDate).subtract(1, 'y').format('YYYY-MM');
let nextYear = moment(fileDate).add(1, 'y').format('YYYY-MM');
let yearLink = fileDate.format('YYYY');
-%>
tags: yearly_note <% yearLink %>
---
<%*
// ❮❮ ⋮⋮ ❯❯
// [[path/to/file|display_text]]
let navStr = `[[Periodic Notes/Yearly/${prevYear}|❮❮]] ⋮⋮ [[Periodic Notes/Yearly/${nextYear}|❯❯]]`;
tR += navStr
%>

## Done this year
```tasks
done after <% moment(fileDate).subtract(1, "y").endOf("year").format('YYYY-MM-DD') %>
done before <% moment(fileDate).add(1, "y").startOf("year").format('YYYY-MM-DD') %>
sort by done reverse
```