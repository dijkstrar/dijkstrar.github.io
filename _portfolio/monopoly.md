--- 
title: 'Monopoly test' 
date: 2020-08-17 
permalink: /portfolio/2020/08/Monopoly/ 
---

<div id="editor">
    print(123)
</div>
<button id="btn">Run Python Test</button>


<script type="text/javascript" src="https://cdn.rawgit.com/brython-dev/brython/stable/www/src/brython.js"></script>
<script type="text/javascript" src="https://cdn.rawgit.com/brython-dev/brython/stable/www/src/brython_stdlib.js"></script>
<script type="text/python">
    from browser import doc, window
    from browser import html

    def exec_python():
        exec(doc['editor'].value)

    doc['btn'].bind('click', exec_python)
</script>