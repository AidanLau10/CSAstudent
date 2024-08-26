---
layout: post
title: Sprint 1 - Javascript
description: Javascript Sprint 1
type: issues
comments: True
permalink: /javascript
---

<button id="textchanger">Click me</button>

<script>
document.getElementById("textchanger").addEventListener("click", function() {
    this.style.backgroundColor = "blue"; // Change "blue" to any color you prefer
  });
</script>