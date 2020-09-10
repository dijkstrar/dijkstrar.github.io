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
          pyodide.runPython(`
                import matplotlib.pyplot as plt
                plt.scatter([0,1],[1,0])
                import io, base64
                buf = io.BytesIO()
                fig.savefig(buf, format='png')
                buf.seek(0)
                img_str = 'data:image/png;base64,' + base64.b64encode(buf.read()).decode('UTF-8')
                `
                );

            document.getElementById("pyplotfigure").src=pyodide.globals.img_str
      });

    </script>
<div id="textfield">A matplotlib figure:</div>
<div id="pyplotdiv"><img id="pyplotfigure"/></div>