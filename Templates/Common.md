---
created: <% tp.file.creation_date() %>
modified: <%+ tp.file.last_modified_date() %>
alias: 
tags: common
source: 
---


------
## ✍内容

 <% await tp.file.move("Notes/Others/" + tp.file.title) %>