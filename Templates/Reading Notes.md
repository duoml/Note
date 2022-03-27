---
annotation-target: Resources/Books/<% (await tp.system.suggester((item) => item.basename+"."+item.extension, app.vault.getFiles())).basename %>.pdf
created: <% tp.file.creation_date() %>
modified: <%+ tp.file.last_modified_date() %>
alias: 
tags: reading
source: 
---
------
## ✍内容
<% await tp.file.move("Notes/Book Notes/" + tp.file.title) %>
 