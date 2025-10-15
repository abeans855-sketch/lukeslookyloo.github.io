<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Click to Reveal QR</title>
  <style>
    body {
      margin: 0;
      background-color: #000;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      cursor: pointer;
      overflow: hidden;
    }

    .container {
      position: relative;
      width: 300px;
      height: 300px;
    }

    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      display: block;
      transition: opacity 0.3s ease;
    }

    .rotating-text {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 300px;
      height: 300px;
      transform: translate(-50%, -50%);
      pointer-events: none;
    }

    .rotating-text span {
      position: absolute;
      left: 50%;
      top: 50%;
      transform-origin: 0 0;
      white-space: nowrap;
      color: white;
      font-family: sans-serif;
      font-size: 1rem;
    }

    @keyframes rotate {
      from {
        transform: rotate(0deg);
      }
      to {
        transform: rotate(360deg);
      }
    }

    .rotating-text {
      animation: rotate 10s linear infinite;
    }
  </style>
</head>
<body>
  <div class="container" onclick="swapImage()">
    <img id="displayImage" src="your-image.jpg" alt="Click to reveal QR" />
    <div id="textRing" class="rotating-text">
      <!-- Text broken into characters and rotated -->
      <!-- Example: "Click the image to reveal QR" -->
    </div>
  </div>

  <script>
    const image = document.getElementById('displayImage');
    const textRing = document.getElementById('textRing');

    // Text to display in a circle
    const message = " Luke's Looky Loo Luke's Looky Loo ";
    const radius = 130; // radius of the circle
    const characters = message.split('');
    const angleStep = 360 / characters.length;

    characters.forEach((char, i) => {
      const span = document.createElement('span');
      span.innerText = char;
      const angle = i * angleStep;
      span.style.transform = `rotate(${angle}deg) translate(${radius}px) rotate(-${angle}deg)`;
      textRing.appendChild(span);
    });

    function swapImage() {
      image.src = "your-qr-code.png";
      textRing.style.display = "none"; // hide rotating text after click
    }
  </script>
</body>
</html>
