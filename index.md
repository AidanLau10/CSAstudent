---
layout: base
title: Student Home 
description: Home Page
hide: true
---

<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
* {box-sizing: border-box}
body {font-family: Verdana, sans-serif; margin:0}
.mySlides {display: none}
img {vertical-align: middle;}

div.gallery {
  margin: 5px;
  border: 1px solid #ccc;
  float: left;
  width: 180px;
}

div.gallery:hover {
  border: 1px solid #777;
}

div.gallery img {
  width: 100%;
  height: auto;
}

div.desc {
  padding: 15px;
  text-align: center;
}

/* Slideshow container */
.slideshow-container {
  max-width: 1000px;
  position: relative;
  margin: auto;
}

/* Next & previous buttons */
.prev, .next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  width: auto;
  padding: 16px;
  margin-top: -22px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

/* Position the "next button" to the right */
.next {
  right: 0;
  border-radius: 3px 0 0 3px;
}

/* On hover, add a black background color with a little bit see-through */
.prev:hover, .next:hover {
  background-color: rgba(0,0,0,0.8);
}

/* Caption text */
.text {
  color: #f2f2f2;
  font-size: 15px;
  padding: 8px 12px;
  position: absolute;
  bottom: 8px;
  width: 100%;
  text-align: center;
}

/* Number text (1/3 etc) */
.numbertext {
  color: #f2f2f2;
  font-size: 12px;
  padding: 8px 12px;
  position: absolute;
  top: 0;
}

/* The dots/bullets/indicators */
.dot {
  cursor: pointer;
  height: 15px;
  width: 15px;
  margin: 0 2px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.active, .dot:hover {
  background-color: #717171;
}

/* Fading animation */
.fade {
  animation-name: fade;
  animation-duration: 1.5s;
}

@keyframes fade {
  from {opacity: .4} 
  to {opacity: 1}
}

/* On smaller screens, decrease text size */
@media only screen and (max-width: 300px) {
  .prev, .next,.text {font-size: 11px}
}

.submenu {
  float: left;
  overflow: hidden;
}

.submenu .sub-btn {
  font-size: 16px;  
  border: none;
  outline: none;
  color: white;
  padding: 14px 16px;
  background-color: inherit;
  font-family: inherit;
  margin: 0;
}

.submenu-content {
  display: none;
  position: absolute;
  background-color: #333;
  min-width: 160px;
  z-index: 1;
}

.submenu-content a {
  float: none;
  color: white;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  text-align: left;
}

.submenu-content a:hover {
  background-color: #ddd;
  color: black;
}

.submenu:hover .submenu-content {
  display: block;
}

}
#factDisplay {
    font-size: 20px;
    margin: 20px 0;
}
#generateBtn {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
}
</style>
</head>
<body>

<div class="navbar" style="padding-bottom: 50px">
  <a href="{{site.baseurl}}/">Home</a>
  <a href="{{site.baseurl}}/planning">Planning</a>

  <a href="{{site.baseurl}}/about">About</a>
</div>
<!-- <iframe style="border-radius:12px" src="https://open.spotify.com/embed/playlist/6MXWK7edsydhiPEs07RDkO?utm_source=generator&theme=0" width="100%" height="352" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe> -->


<div style="padding-bottom: 50px">
  <img src="images/frontpage/freeform.png" style="width:100%">
  <h3>In my freeform diagram, I drew my family and I. I also drew clothes because I like finding new pieces to wear, headphones becasue I like listening to music, and a gaming setup because I like playing games.</h3>
</div>

<div style="padding-bottom: 50px">
  <h3>Here are my classes for trimester 1</h3>
  <ol>
    <li>AP CSA</li>
    <li>AP Stats</li>
    <li>Chinese</li>
    <li>AP Physics</li>
    <li>APEL</li>
  </ol>
</div>



<div class="slideshow-container">

<div class="mySlides fade">
  <div class="numbertext">1 / 3</div>
  <img src="images/frontpage/lucki.png" style="width:100%">
  <div class="text">lucki</div>
</div>

<div class="mySlides fade">
  <div class="numbertext">2 / 3</div>
  <img src="images/frontpage/grant.jpeg" style="width:100%">
  <div class="text">grentperez</div>
</div>

<div class="mySlides fade">
  <div class="numbertext">3 / 3</div>
  <img src="images/frontpage/w2e.jpeg" style="width:100%">
  <div class="text">wave to earth</div>
</div>

<a class="prev" onclick="plusSlides(-1)">❮</a>
<a class="next" onclick="plusSlides(1)">❯</a>

</div>
<br>

<div style="text-align:center">
  <span class="dot" onclick="currentSlide(1)"></span> 
  <span class="dot" onclick="currentSlide(2)"></span> 
  <span class="dot" onclick="currentSlide(3)"></span> 
</div>

<div id="factDisplay">Click the button to see a fun fact!</div>
<button id="generateBtn">Generate Fun Fact</button>
<script>
let slideIndex = 1;
showSlides(slideIndex);

function plusSlides(n) {
  showSlides(slideIndex += n);
}

function currentSlide(n) {
  showSlides(slideIndex = n);
}

function showSlides(n) {
  let i;
  let slides = document.getElementsByClassName("mySlides");
  let dots = document.getElementsByClassName("dot");
  if (n > slides.length) {slideIndex = 1}    
  if (n < 1) {slideIndex = slides.length}
  for (i = 0; i < slides.length; i++) {
    slides[i].style.display = "none";  
  }
  for (i = 0; i < dots.length; i++) {
    dots[i].className = dots[i].className.replace(" active", "");
  }
  slides[slideIndex-1].style.display = "block";  
  dots[slideIndex-1].className += " active";
}

document.addEventListener('DOMContentLoaded', function() {
    const facts = [
        "I can solve a Rubiks cube. My fastest time was 6 seconds",
        "My favorite subject is math",
        "I'm going to 2 concerts in September: Rocco and wave to earth",
        "I can build keyboards.",
    ];

    const factDisplay = document.getElementById('factDisplay');
    const generateBtn = document.getElementById('generateBtn');

    generateBtn.addEventListener('click', function() {
        const randomIndex = Math.floor(Math.random() * facts.length);
        factDisplay.textContent = facts[randomIndex];
    });
});
</script>

</body>
</html> 