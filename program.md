program.md(below)                                                                                                                        
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dynamic Image Slider</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center; 
      height: 100vh;
      margin: 0;
      background: #f1f1f1;
    }

    h1 {
      margin-bottom: 20px;
      color: #333;
    }

    .slider {
      width: 80%;
      max-width: 600px;
      position: relative;
      overflow: hidden;
      border-radius: 15px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
    }

    .slides {
      display: flex;
      transition: transform 0.6s ease-in-out;
    }

    .slides img {
      width: 100%;
      border-radius: 15px;
    }

    .caption {
      margin-top: 10px;
      font-size: 18px;
      color: #555;
      text-align: center;
      min-height: 24px;
    }

    .prev, .next {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background-color: rgba(0,0,0,0.5);
      color: #fff;
      border: none;
      padding: 10px;
      cursor: pointer;
      border-radius: 50%;
      font-size: 18px;
    }

    .prev { left: 10px; }
    .next { right: 10px; }

    .dots {
      text-align: center;
      margin-top: 10px;
    }

    .dot {
      height: 10px;
      width: 10px;
      margin: 5px;
      background-color: #bbb;
      border-radius: 50%;
      display: inline-block;
      cursor: pointer;
    }

    .active {
      background-color: #333;
    }
  </style>
</head>
<body>

  <h1>Dynamic Image Slider</h1>

  <div class="slider">
    <div class="slides" id="slideContainer">
      <!-- Images will be dynamically loaded here -->
    </div>
    <button class="prev" onclick="moveSlide(-1)">❮</button>
    <button class="next" onclick="moveSlide(1)">❯</button>
  </div>

  <div class="caption" id="captionText"></div>
  <div class="dots" id="dotsContainer"></div>

  <script>
    const images = [
      {
        src: "https://picsum.photos/id/1018/800/400",
        caption: "Mountain View"
      },
      {
        src: "https://picsum.photos/id/1020/800/400",
        caption: "Wild Animal"
      },
      {
        src: "https://picsum.photos/id/1024/800/400",
        caption: "Wild Bird"
      },
      {
        src: "https://picsum.photos/id/1037/800/400",
        caption: "Sun Shine"
      }
    ];

    const slideContainer = document.getElementById("slideContainer");
    const dotsContainer = document.getElementById("dotsContainer");
    const captionText = document.getElementById("captionText");
    let currentIndex = 0;

    images.forEach((imgObj, index) => {
      const img = document.createElement("img");
      img.src = imgObj.src;
      slideContainer.appendChild(img);

      const dot = document.createElement("span");
      dot.classList.add("dot");
      dot.addEventListener("click", () => showSlide(index));
      dotsContainer.appendChild(dot);
    });

    const totalSlides = images.length;
    const dots = document.querySelectorAll(".dot");

    function showSlide(index) {
      currentIndex = (index + totalSlides) % totalSlides;
      slideContainer.style.transform = translateX(-${currentIndex * 100}%);
      dots.forEach(dot => dot.classList.remove("active"));
      dots[currentIndex].classList.add("active");
      captionText.textContent = images[currentIndex].caption;
    }

    function moveSlide(step) {
      showSlide(currentIndex + step);
    }

    setInterval(() => {
      moveSlide(1);
    }, 3000);

    showSlide(currentIndex);
  </script>

</body>
</html>
