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
      pyodide.loadPackage(['urllib.request','json']).then(() => {
          pyodide.runPython(`
                import urllib.request, json 
                  with urllib.request.urlopen('http://ipinfo.io/json') as url:
                        data = json.loads(url.read().decode())
                        data['latitude'] = data['loc'].split(',')[0]
                        data['longitude']=data['loc'].split(',')[1]
                        print(data)
                `
                );

          document.getElementById("pyplotfigure").src=pyodide.globals.img_str

      });});

</script>


<div id="textfield">A matplotlib figure:</div>
<div id="pyplotdiv"><img id="pyplotfigure"/></div>