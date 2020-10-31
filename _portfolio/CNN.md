--- 
title: 'CNN' 
date: 2020-10-24 
permalink: /portfolio/2020/10/CNN/ 
---

Trial of CNN new (!) Only canvas now!

<div id="canvas">Click to draw<br/></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@2.0.0/dist/tf.min.js"></script>

<script>
function create_container() {
    function createCanvas(parent, width, height) {
        var canvas = {};
        canvas.node = document.createElement('canvas');
        canvas.context = canvas.node.getContext('2d');
        canvas.node.width = width || 100;
        canvas.node.height = height || 100;
        parent.appendChild(canvas.node);
        return canvas;
    }

    function init(container, width, height, fillColor) {
        var canvas = createCanvas(container, width, height);
        var ctx = canvas.context;
        
        ctx.fillCircle = function(x, y, radius, fillColor) {
            this.fillStyle = fillColor;
            this.beginPath();
            this.moveTo(x, y);
            this.arc(x, y, radius, 0, Math.PI * 2, false);
            this.fill();
        };
        ctx.clearTo = function(fillColor) {
            ctx.fillStyle = fillColor;
            ctx.fillRect(0, 0, width, height);
        };
        ctx.clearTo(fillColor || "#ddd");

        
        canvas.node.onmousemove = function(e) {
            if (!canvas.isDrawing) {
               return;
            }
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            var radius = 10; 
            var fillColor = '#FF0000';
            ctx.fillCircle(x, y, radius, fillColor);
        };
        canvas.node.onmousedown = function(e) {
            canvas.isDrawing = true;
        };
        canvas.node.onmouseup = function(e) {
            canvas.isDrawing = false;
        };
        ctx.lineWidth = 2;
				ctx.strokeStyle="#000000";
				ctx.strokeRect(0, 0, width, height);
         
        return canvas
    }

    var container = document.getElementById('canvas');
    var canvas  = init(container, 200,200, '#0000');
		return canvas
}

var canvas = create_container();
</script>

<button onclick="predict(canvas)">Predict!</button> 
<button onclick="erase(canvas)">Erase!</button> 
