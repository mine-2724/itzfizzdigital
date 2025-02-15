# itzfizzdigital

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Funky Anime Hero Section with Music</title>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <!-- GSAP Library -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
  <style>
    /* Global Reset */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Poppins', sans-serif;
      overflow-x: hidden;
      color: #fff;
      background: #000;
    }
    /* Animated Gradient Background */
    .hero {
      position: relative;
      width: 100%;
      height: 100vh;
      background: linear-gradient(45deg, #ff0080, #ff8c00, #40e0d0, #8a2be2);
      background-size: 600% 600%;
      animation: gradientBG 8s ease infinite;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 20px;
    }
    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    /* Dark Overlay for better text contrast */
    .hero::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.3);
      z-index: 1;
    }
    /* Hero Text */
    .hero-text {
      position: relative;
      z-index: 2;
      margin-bottom: 40px;
    }
    .hero-text h1 {
      font-family: 'Fredoka One', cursive;
      font-size: 4rem;
      color: #fff;
      text-shadow: 3px 3px 6px rgba(0,0,0,0.8);
      margin-bottom: 20px;
    }
    .hero-text p {
      font-size: 1.5rem;
      color: #f0f0f0;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
    }
    /* Image Gallery */
    .image-gallery {
      position: relative;
      display: flex;
      gap: 20px;
      z-index: 2;
    }
    .image-gallery img {
      width: 300px;
      height: 200px;
      object-fit: cover;
      border-radius: 12px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.3);
      transition: transform 0.3s ease, filter 0.3s ease;
      cursor: pointer;
      /* Default vector-like style */
      filter: grayscale(100%) contrast(150%);
    }
    .image-gallery img.active {
      filter: none;
    }
    /* Music Player (hidden controls) */
    #backgroundMusic {
      display: none;
    }
  </style>
</head>
<body>
  <section class="hero">
    <div class="hero-text">
      <h1 id="heroTitle">Unleash Your Anime Vibes</h1>
      <p id="heroSubtitle">Funky, Fresh & Full of Energy</p>
    </div>
    <div class="image-gallery">
      <!-- Anime-themed images -->
      <img src="anime1.jpg" alt="Anime Funky 1" class="hero-img" data-index="0">
      <img src="anime2.jpg" alt="Anime Funky 2" class="hero-img" data-index="1">
      <img src="anime3.jpg" alt="Anime Funky 3" class="hero-img" data-index="2">
    </div>
  </section>

  <!-- Auto-playing Background Music -->
  <audio id="backgroundMusic" autoplay loop>
    <source src="https://www.bensound.com/bensound-music/bensound-funkyelement.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <script>
    // Attempt to auto-play music
    window.addEventListener('load', () => {
      const music = document.getElementById('backgroundMusic');
      music.play().catch(error => {
        console.log("Autoplay failed, will play after user interaction", error);
      });
    });

    // GSAP Initial Animations for Text and Images
    gsap.from(".hero-text h1", { duration: 1, y: -50, opacity: 0, ease: "power2.out" });
    gsap.from(".hero-text p", { duration: 1, y: 50, opacity: 0, ease: "power2.out", delay: 0.5 });
    gsap.from(".hero-img", { duration: 1, opacity: 0, scale: 0.8, stagger: 0.3, delay: 1 });

    // Interactive Image Effects
    const images = document.querySelectorAll(".hero-img");
    images.forEach(img => {
      // On mouse enter: set the image as active and change text style
      img.addEventListener("mouseenter", () => {
        images.forEach(other => {
          if (other !== img) {
            other.classList.remove("active");
          }
        });
        img.classList.add("active");
        document.getElementById("heroTitle").style.color = "#e67e22";
        document.getElementById("heroSubtitle").style.fontStyle = "italic";
      });
      // On mouse leave: reset styles
      img.addEventListener("mouseleave", () => {
        images.forEach(other => {
          other.classList.remove("active");
          other.style.transform = "";
        });
        document.getElementById("heroTitle").style.color = "#fff";
        document.getElementById("heroSubtitle").style.fontStyle = "normal";
      });
      // Mouse movement effect: active image follows mouse slightly
      img.addEventListener("mousemove", (e) => {
        const rect = img.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const offsetX = (x / rect.width - 0.5) * 20;
        const offsetY = (y / rect.height - 0.5) * 20;
        img.style.transform = `translate(${offsetX}px, ${offsetY}px) scale(1.05)`;
      });
    });
  </script>
</body>
</html>
