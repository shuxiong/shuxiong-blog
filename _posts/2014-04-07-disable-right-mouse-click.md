---
published: true
layout: post
title: "How to disable right mouse click"
date: 2014-04-07 01:19
comments: false
categories: ['web']
---

##How to disable right mouse click##

Sometimes, we want to disable right mouse click, so we can achieve this by simplely adding a few lines of js.

```javascript
<!-- disable_right_click.html BEGIN -->
<script type="text/javascript">
    document.body.oncontextmenu=function(){return false;};
    document.body.ondragstart=function(){return false;};
    document.body.onselectstart=function(){return false;};
    document.body.onbeforecopy=function(){return false;};
    document.body.onselect=function(){document.selection.empty();};
    document.body.oncopy=function(){document.select.empty();};
</script>
<!-- disable_right_click.html END -->
```
