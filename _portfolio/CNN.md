--- 
title: 'CNN' 
date: 2020-10-24 
permalink: /portfolio/2020/10/CNN/ 
---

Trial of CNN

<div id="canvas">Click to draw<br/></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@2.0.0/dist/tf.min.js"></script>
<button onclick="predict(canvas)">Predict!</button> 
<button onclick="erase(canvas)">Erase!</button> 
<script> 
function create_container() {
    // Creates a new canvas element and appends it as a child
    // to the parent element, and returns the reference to
    // the newly created canvas element
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
        // define a custom fillCircle method
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
        // bind mouse events
        canvas.node.onmousemove = function(e) {
            if (!canvas.isDrawing) {
               return;
            }
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            var radius = 10; // or whatever
            var fillColor = '#FF0000';
            ctx.fillCircle(x, y, radius, fillColor);
        };
        canvas.node.onmousedown = function(e) {
            canvas.isDrawing = true;
        };
        canvas.node.onmouseup = function(e) {
            canvas.isDrawing = false;
        };
        return canvas
    }
    var container = document.getElementById('canvas');
    var canvas  = init(container, 200,200, '#0000');
		return canvas
}
var canvas = create_container();
function predict(canvas){
var gfg = canvas.node.getContext("2d")
var g =  gfg.getImageData(0, 0, 200, 200); 
const tens = tf.browser.fromPixels(g,1).resizeNearestNeighbor([28, 28]).div(255)
console.log(tens.print())
console.log(tens.shape)
console.log('going to load model')
let model = load_model();
console.log('finished loading')
model.then(model => {
    const prediction = model.predict(tens.reshape([1, 28, 28, 1]),);
    console.log('done?')
    console.log(prediction);});}
async function load_model() {
    let m = await tf.loadLayersModel('files\model.json')
    console.log(typeof m)
    console.log('loading?')
    return m;
}
let model = load_model();
function erase(canvas){
const context = canvas.node.getContext('2d');
context.clearRect(0, 0, canvas.node.width, canvas.node.height);
}
</script>
