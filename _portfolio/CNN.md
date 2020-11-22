--- 
title: 'CNN For Handwritten Digits' 
date: 2020-10-24 
permalink: /portfolio/2020/10/CNN/ 
---

This page contains a number recognizer. For this project I have created a Convolutional Neural Network (CNN) in order to recognize handwritten digits. The CNN has been trained on the [mnist dataset](https://en.wikipedia.org/wiki/MNIST_database), with a CNN of three convolutional layers, with filter sizes of 5, 4 and 3 (5, 10 and 15 filters). Moreover we activate each convolutional layer with the Relu function, and MaxPool consequently. Below a brief instruction is given on how to use the tool, afterwards you can try it yourself. Lastly, information on model quality and feature engineeering is supplied.

#### Instructions
In order to draw please hold down the left-mouse button in the canvas. The color of the marker will be red. Once you have finished drawing the digit, you can release the left-mouse button and click "Predict!". A plot will be shown which displays the probabilities of classification (e.g. the model is x% sure the drawn digit resembles digit y). Whenever you want to re-draw adjust your drawing or draw another digit, please wipe the canvas, by using the "Erase!" button. After the canvas has been cleared, you can draw again. Pushing buttons multiple times after eachother yields problems, in that case please refresh the site. Try it yourself!

<div id="canvas">Click to draw<br/></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@2.0.0/dist/tf.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.5.0/Chart.min.js"></script>
<body>
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

<script>
function erase(canvas){
    const context = canvas.node.getContext('2d');
    context.clearRect(0, 0, canvas.node.width, canvas.node.height);
    context.strokeStyle="#000000";
    context.strokeRect(0, 0, canvas.node.width, canvas.node.height);
    
   	this.bar_chart_object.destroy();
    
    
}
</script>

<script>
async function load_model() {
    let m = await tf.loadLayersModel('https://raw.githubusercontent.com/dijkstrar/dijkstrar.github.io/master/files/model.json','https://raw.githubusercontent.com/dijkstrar/dijkstrar.github.io/master/files/group1-shard1of1.bin');
    return m;
}
</script>

<script>
async function predict(canvas){
    var gfg = canvas.node.getContext("2d");
    var g =  gfg.getImageData(0, 0, 200, 200); 
    const tens = tf.browser.fromPixels(g,1).resizeNearestNeighbor([28, 28]).div(255);
    let model = load_model();
    console.log('finished loading');

    model.then(model => {
        const prediction = model.predict(tens.reshape([1, 28, 28, 1]),);
    	create_chart(Array.from(prediction.dataSync()));
        showChart();
    });
    
}
</script>

<script>
function determine_colors(arr){
	max_num = Math.max.apply(Math, arr);
    newArr =[];
    for(i=0; i<arr.length; i++){
    	if (arr[i]==max_num){
        	newArr.push('#000000');
        }
        else newArr.push('#666a70');
    }
    return newArr;
}
</script>

<script>
function convert(arr){
    newArr =[];
    for(i=0; i<arr.length; i++){
        newArr.push(arr[i].toFixed(2));
    }
    return newArr;
}
</script>

<script>
async function create_chart(prediction){
    bar_chart_object = new Chart(document.getElementById("bar-chart"), {
        type: 'bar',
        data: {
        	labels: Array.from(Array(10).keys()),
        	datasets: [
        			{
          label: "Probability",
          backgroundColor: determine_colors(prediction),
          data: convert(prediction)
        }
      ]
        },
        options: {
        scales: {
            xAxes: [{
                barPercentage: 1,
                gridLines: {
                    display:false
                }
            }],
            yAxes: [{
            ticks: {
                max: 1},
                gridLines: {
                    display:false
                }   
            }]
        },
        legend: { display: false },
        responsive: false,
        maintainAspectRatio: true,
        title: {
            display: true,
            text: 'Predicted Number from Drawing'
        }
        }
    });
	return bar_chart_object;
}
</script>


<script>
    function showChart(){
        document.getElementById('bar-chart').style.display='block';
    }
</script>

<button onclick="predict(canvas)">Predict!</button> 
<button onclick="erase(canvas)">Erase!</button> 
<div><canvas id="bar-chart"></canvas></div>

</body>

### Goal of the Project
As the scope of this project was to aim to launch a machine learning model, not much attention has been devoted towards selecting the best model. The main goal was to provide an environment in which users can test the machine learning model in an interactive manner. As drawings in a JavaScript canvas do not contain shade, the network had to be trained to handle pixels in which was drawn, irrespective of their color intensity. Therefore, for the sake of feature engineering, all shaded areas of the handwritten digits in the mnist dataset have been decoded into the most intense color within the digit, as displayed below: ![Getting Started](</images/mnist_digit_transformation.PNG>)

### Model Training
As for the model itself, a relatively simple CNN has been applied, namely one with filter sizes of 5, 4 and 3 ( with respectively 5, 10 and 15 number of filters). After each filter we apply a Relu activation function, and MaxPool over the corresponding result. At the end we create a fully connected layer of size 256, and a sigmoid activation function. Afterwards we derive predictions with the help of the softmax activation function (which assigns probabilities to the digits 0-9 for the drawn digit). As for the training, Adam Optimizer has been used with a learning rate of 0.0005, as to have a proper trade-off between exploitation and exploration. Moreover, a batch-size of 400 has been used, and we train the model for 50 epochs. This training set-up ensures a relatively good model for short training times. It is indeed possible to use a more extensive model, however that would yield more training times, and the increase in accuracy would not be that significant. For the current model, the following model_loss and accuracies have been obtained for the training and validation set:  ![Getting Started](</images/mnist_accuracies.PNG>). As for the test set, an accuracy of 0.9695 has been obtained, which is high! 

### Inaccuracies of the Model
When drawing digits yourself, it is possible that the trained model will incorrectly classify your drawn digit, this might be due to 'bias' in the training set. The mnist-dataset contains mostly hand-drawn digits, centered in the screen and have a certain style. For example, it is possible to draw a digit in a style the CNN has never seen, and it will for example incorrectly classify (e.g. when drawing a one as '1' instead of |). 
As for an example of how digits in the mnist-dataset are drawn, pleeas inspect the following examples: ![Getting Started](</images/mnist_examples.PNG>)