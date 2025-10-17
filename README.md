<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Click to Reveal QR</title>

  <!-- Preload QR code for instant switch -->
  <link rel="preload" href="your-qr-code.png" as="image">

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
      transition: transform 0.4s ease;
    }

    .container:hover {
      transform: scale(1.05);
    }

    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      display: block;
      transition: opacity 0.4s ease;
      opacity: 1;
    }

    .rotating-text {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 300px;
      height: 300px;
      transform: translate(-50%, -50%);
      pointer-events: none;
      animation: rotate 10s linear infinite;
    }

    .rotating-text span {
      position: absolute;
      left: 50%;
      top: 50%;
      transform-origin: 0 0;
      white-space: nowrap;
      color: white;
      font-family: sans-serif;
      font-size: calc(10px + 0.5vw);
      text-shadow: 0 0 6px rgba(255, 255, 255, 0.7);
    }

    @keyframes rotate {
      from { transform: rotate(0deg); }
      to { transform: rotate(360deg); }
    }
  </style>
</head>
<body>
  <div class="container" onclick="swapImage()">
    <img id="displayImage" src="luke.jpg" alt="Click to reveal QR" />
    <div id="textRing" class="rotating-text"></div>
  </div>

  <script>
    const image = document.getElementById('displayImage');
    const textRing = document.getElementById('textRing');
    let showingQR = false;

    // Text that circles around
    const message = " Click to Reveal QR • Luke's Looky Loo • ";
    const radius = 130; // radius of text circle
    const characters = message.split('');
    const angleStep = 360 / characters.length;

    // Build rotating circular text
    characters.forEach((char, i) => {
      const span = document.createElement('span');
      span.innerText = char;
      const angle = i * angleStep;
      span.style.transform = `rotate(${angle}deg) translate(${radius}px) rotate(-${angle}deg)`;
      textRing.appendChild(span);
    });

    // Smooth image toggle
    function swapImage() {
      image.style.opacity = 0;
      setTimeout(() => {
        if (!showingQR) {
          image.src = "youtube_qr.png";
          textRing.style.display = "none";
        } else {
          image.src = "Luke.jpg";
          textRing.style.display = "block";
        }
        showingQR = !showingQR;
        image.style.opacity = 1;
      }, 300);
    }
  </script>
</body>
</html>
