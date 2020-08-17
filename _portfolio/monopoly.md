--- 
title: 'Monopoly test' 
date: 2020-08-17 
permalink: /portfolio/2020/08/Monopoly/ 
---

<div id="editor">
    print(123)
</div>
<button id="btn">Run Python</button>

...

<script type="text/javascript" src="https://cdn.rawgit.com/brython-dev/brython/stable/www/src/brython.js"></script>
<script type="text/javascript" src="https://cdn.rawgit.com/brython-dev/brython/stable/www/src/brython_stdlib.js"></script>
<script type="text/python">
    def test():
        print(5+5)

    doc['btn'].bind('click', test)
</script>