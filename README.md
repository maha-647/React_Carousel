# Ex05 Image Carousel
## Date:15/09/2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
```
#main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./App.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
```
#app.jsx
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {

  const slides = [
    {
      image: "https://picsum.photos/id/1015/1200/700",
      title: "Into the Mountains",
      text: "Where the sky meets the earth"
    },
    {
      image: "https://picsum.photos/id/1018/1200/700",
      title: "Dreamy Escape",
      text: "A peaceful moment in nature"
    },
    {
      image: "https://picsum.photos/id/1025/1200/700",
      title: "Little Explorer",
      text: "Adventure is everywhere"
    },
    {
      image: "https://picsum.photos/id/1035/1200/700",
      title: "Golden Journey",
      text: "Collect moments, not things"
    }
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  const nextSlide = () => {
    setCurrentIndex((prev) =>
      prev === slides.length - 1 ? 0 : prev + 1
    );
  };

  const prevSlide = () => {
    setCurrentIndex((prev) =>
      prev === 0 ? slides.length - 1 : prev - 1
    );
  };

  useEffect(() => {
    const interval = setInterval(nextSlide, 3000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="page">

      {/* Background Effects */}
      <div className="orb orb1"></div>
      <div className="orb orb2"></div>
      <div className="orb orb3"></div>

      <div className="container">

        {/* Header */}
        <div className="header">

          <p className="small-title">
            ✦ VISUAL JOURNEY ✦
          </p>

          <h1>
            Dreamy <span>Gallery</span>
          </h1>

          <p className="subtitle">
            Explore beautiful moments, one slide at a time.
          </p>

        </div>

        {/* Carousel */}
        <div className="carousel-wrapper">

          <div className="carousel">

            <img
              key={currentIndex}
              src={slides[currentIndex].image}
              alt={slides[currentIndex].title}
              className="slide"
            />

            <div className="overlay"></div>

            {/* Image Information */}
            <div className="content">

              <p className="number">
                0{currentIndex + 1} / 0{slides.length}
              </p>

              <h2>
                {slides[currentIndex].title}
              </h2>

              <p>
                {slides[currentIndex].text}
              </p>

            </div>

            {/* Previous */}
            <button
              className="nav-btn prev"
              onClick={prevSlide}
            >
              ←
            </button>

            {/* Next */}
            <button
              className="nav-btn next"
              onClick={nextSlide}
            >
              →
            </button>

          </div>

          {/* Dots */}
          <div className="dots">

            {slides.map((_, index) => (

              <button
                key={index}
                className={
                  currentIndex === index
                    ? "dot active"
                    : "dot"
                }
                onClick={() => setCurrentIndex(index)}
              ></button>

            ))}

          </div>

        </div>

        {/* Footer */}
        <div className="footer">

          <span>React</span>
          <span>•</span>
          <span>Image Carousel</span>
          <span>•</span>
          <span>2026</span>

        </div>

      </div>

    </div>
  );
}

export default App;


```
```

#app.css
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=Playfair+Display:wght@500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "DM Sans", sans-serif;
  background: #120d1f;
  color: white;
}

.page {
  min-height: 100vh;
  overflow: hidden;
  position: relative;
  background:
    radial-gradient(circle at 20% 20%, #352050, transparent 30%),
    radial-gradient(circle at 80% 80%, #202b50, transparent 30%),
    linear-gradient(135deg, #100b1c, #191128, #0d1528);
}

.container {
  max-width: 1150px;
  margin: auto;
  padding: 60px 25px;
  position: relative;
  z-index: 2;
}

.header {
  text-align: center;
  margin-bottom: 40px;
}

.small-title {
  color: #dca9ff;
  font-size: 12px;
  letter-spacing: 5px;
  margin-bottom: 15px;
}

.header h1 {
  font-family: "Playfair Display", serif;
  font-size: 65px;
  margin-bottom: 12px;
}

.header h1 span {
  background: linear-gradient(90deg, #ffb3df, #cba7ff, #91c9ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.subtitle {
  color: #bcb3c9;
}

.carousel-wrapper {
  max-width: 1000px;
  margin: auto;
}

.carousel {
  position: relative;
  height: 560px;
  overflow: hidden;
  border-radius: 28px;
  border: 1px solid rgba(255,255,255,0.15);
  box-shadow: 0 30px 80px rgba(0,0,0,0.5);
}

.slide {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  animation: zoomIn 0.8s ease;
}

@keyframes zoomIn {
  from {
    transform: scale(1.08);
    opacity: 0.5;
  }

  to {
    transform: scale(1);
    opacity: 1;
  }
}

.overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    90deg,
    rgba(8,5,15,0.85),
    rgba(8,5,15,0.1)
  );
}

.content {
  position: absolute;
  left: 55px;
  bottom: 55px;
}

.number {
  color: #ddb4ff;
  letter-spacing: 3px;
  margin-bottom: 15px;
}

.content h2 {
  font-family: "Playfair Display", serif;
  font-size: 48px;
  margin-bottom: 10px;
}

.content p:last-child {
  color: #e1dce6;
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 55px;
  height: 55px;
  border-radius: 50%;
  border: 1px solid rgba(255,255,255,0.25);
  background: rgba(255,255,255,0.12);
  color: white;
  font-size: 25px;
  cursor: pointer;
  transition: 0.3s;
}

.nav-btn:hover {
  background: rgba(255,255,255,0.3);
  transform: translateY(-50%) scale(1.1);
}

.prev {
  left: 25px;
}

.next {
  right: 25px;
}

.dots {
  display: flex;
  justify-content: center;
  gap: 9px;
  margin-top: 25px;
}

.dot {
  width: 9px;
  height: 9px;
  border: none;
  border-radius: 20px;
  background: #5c5367;
  cursor: pointer;
  transition: 0.4s;
}

.dot.active {
  width: 32px;
  background: linear-gradient(90deg, #ffabd9, #b99aff);
}

.footer {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 35px;
  color: #776d82;
  font-size: 12px;
}

.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(90px);
  opacity: 0.35;
}

.orb1 {
  width: 300px;
  height: 300px;
  background: #d88cff;
  top: -100px;
  left: -80px;
}

.orb2 {
  width: 350px;
  height: 350px;
  background: #6d8cff;
  right: -100px;
  bottom: -100px;
}

.orb3 {
  width: 200px;
  height: 200px;
  background: #ff8fcf;
  left: 45%;
  top: 45%;
}

@media (max-width: 768px) {
  .container {
    padding: 40px 15px;
  }

  .carousel {
    height: 430px;
  }

  .header h1 {
    font-size: 45px;
  }

  .content {
    left: 30px;
    bottom: 35px;
  }

  .content h2 {
    font-size: 34px;
  }
}
```
```
#index.css
html,
body,
#root {
  margin: 0;
  padding: 0;
  width: 100%;
  min-height: 100%;
}
```


## OUTPUT

<img width="1042" height="561" alt="image" src="https://github.com/user-attachments/assets/68026aab-ddfc-4eeb-9a8a-e5144d55883c" />
<img width="1037" height="561" alt="image" src="https://github.com/user-attachments/assets/fb901dec-035f-4869-9ffe-79d73a5de495" />
<img width="1042" height="557" alt="image" src="https://github.com/user-attachments/assets/7376c2d4-2958-4c03-8965-35fe144c4c00" />
<img width="1042" height="557" alt="image" src="https://github.com/user-attachments/assets/206679f5-e96a-4cd7-801e-caf347904ff7" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
