<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Machine Learning Web App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 20px;
        }

        #inputData {
            margin-bottom: 10px;
        }

        #output {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>Machine Learning Web App</h1>

    <label for="inputData">Enter Data:</label>
    <input type="text" id="inputData" placeholder="Enter numeric data">
    <button onclick="predict()">Predict</button>

    <div id="output"></div>

    <!-- TensorFlow.js library -->
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>

    <script>
        // Define a simple linear regression model
        const model = tf.sequential();
        model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
        model.compile({ optimizer: 'sgd', loss: 'meanSquaredError' });

        // Train the model with some example data
        const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
        const ys = tf.tensor2d([2, 4, 6, 8], [4, 1]);

        model.fit(xs, ys, { epochs: 100 }).then(() => {
            console.log('Model trained');
        });

        // Function to predict based on user input
        function predict() {
            const inputData = document.getElementById('inputData').value;
            const inputTensor = tf.tensor2d([parseFloat(inputData)], [1, 1]);
            const output = model.predict(inputTensor);

            const outputElement = document.getElementById('output');
            outputElement.innerHTML = `Predicted Output: ${output.dataSync()[0].toFixed(2)}`;

            inputTensor.dispose();
            output.dispose();
        }
    </script>
</body>
</html>
