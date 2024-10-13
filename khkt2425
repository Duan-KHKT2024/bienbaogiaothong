<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Traffic Sign Recognition</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin: 20px;
    }
    h1 {
      font-size: 2em;
    }
    p {
      font-size: 1.2em;
    }
    #video {
      width: 100%;
      max-width: 600px;
      height: auto;
    }
    #label-container {
      margin-top: 20px;
      font-size: 1.2em;
    }

    /* Make the layout responsive */
    @media screen and (max-width: 600px) {
      h1 {
        font-size: 1.5em;
      }
      p {
        font-size: 1em;
      }
      #label-container {
        font-size: 1em;
      }
    }
  </style>
</head>
<body>
  <h1>Traffic Sign Recognition</h1>
  <p>Allow camera access to start recognizing traffic signs.</p>

  <!-- Video feed -->
  <video id="video" autoplay playsinline></video>
  
  <!-- Display prediction -->
  <div id="label-container"></div>

  <!-- Teachable Machine Model URL -->
  <script type="text/javascript">
    const URL = "https://teachablemachine.withgoogle.com/models/YOUR_MODEL_URL/"; // Replace with your model URL

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
      const modelURL = URL + "model.json";
      const metadataURL = URL + "metadata.json";

      // Load the model
      model = await tmImage.load(modelURL, metadataURL);
      maxPredictions = model.getTotalClasses();

      // Access the webcam
      const flip = true; // whether to flip the webcam
      webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
      await webcam.setup(); // request access to the webcam
      await webcam.play();
      window.requestAnimationFrame(loop);

      // Append elements to the DOM
      document.getElementById("video").appendChild(webcam.canvas);
      labelContainer = document.getElementById("label-container");
      for (let i = 0; i < maxPredictions; i++) { // create elements to hold prediction labels
        labelContainer.appendChild(document.createElement("div"));
      }
    }

    async function loop() {
      webcam.update(); // update the webcam frame
      await predict();
      window.requestAnimationFrame(loop);
    }

    // Run the image through the model
    async function predict() {
      const prediction = await model.predict(webcam.canvas);

      for (let i = 0; i < maxPredictions; i++) {
        const classPrediction = prediction[i].className + ": " + Math.round(prediction[i].probability * 100) + "%";
        labelContainer.childNodes[i].innerHTML = classPrediction;
      }
    }

    window.onload = init;
  </script>
</body>
</html>
