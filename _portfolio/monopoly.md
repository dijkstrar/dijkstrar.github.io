--- 
title: 'Monopoly test' 
date: 2020-08-17 
permalink: /portfolio/2020/08/Monopoly/ 
---
<script type="text/javascript">
          // set the pyodide files URL (packages.json, pyodide.asm.data etc)
          window.languagePluginUrl = 'https://pyodide-cdn2.iodide.io/v0.15.0/full/';
      </script>
<script src="https://pyodide-cdn2.iodide.io/v0.15.0/full/pyodide.js"></script>


<script type="text/javascript">
      languagePluginLoader.then(() => {
          pyodide.runPython(`my_string = "This is a python string." `);

          document.getElementById("textfield").innerText = pyodide.globals.my_string;
      });

    </script>
<div id="textfield"></div>