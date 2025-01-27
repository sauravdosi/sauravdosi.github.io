---
layout: about
title: about
permalink: /
subtitle: <a href="#">AI and Robotics Researcher. ML Engineer. Multimodal AI.</a>

profile:
  align: right
  image: home_profile.jpeg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>saurav [dot] dosi [at]</p>
    <p>utdallas [dot] edu</p>

news: true # includes a list of news items
selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---
<div class="hero" id="hero">
  <p id="scrambledText">mH, lleocme waun fleloh!</p>
</div>

I am an AI Researcher and Industry Professional with over 2 years of academic research and over 3 years of industry experience. I am currently pursuing my Master's in Computer Science at [the University of Texas at Dallas](https://engineering.utdallas.edu/), with an expected graduation in December 2025.

At UTD, I work as an AI Researcher at the [Intelligent Robotics and Vision Lab](https://labs.utdallas.edu/irvl/), advised by [Dr. Yu Xiang](https://yuxng.github.io/), focusing on efficient long-horizon Robot Exploration. My broader research interests lie in **Multimodal AI** and its intersection with **Robotics**.

Previously, I gained extensive industry experience at organizations like:

- [ISN](https://www.isnetworld.com/en/): Data Science (NLP) Summer Internship
- [Quantrium AI](https://www.quantrium.ai/) (Startup): ML Engineer for 2 years
- [Mirrag AI](https://mirrag.in/) (Startup): AI Engineer
- [Express Analytics](https://www.expressanalytics.com/): Data Science Internship

In addition, I am currently a Teaching Assistant for CS3345 - Data Structures and Algorithms, under [Dr. Sridhar Alagar](https://profiles.utdallas.edu/sridhar).

I earned my BTech in Mechanical Engineering with a Minor in Machine Learning from [Indian Institute of Technology Dharwad](https://www.iitdh.ac.in/). My [undergraduate thesis](https://link.springer.com/chapter/10.1007/978-3-031-05767-0_2) on a vision-based fruit assortment machine with optimal computation was published in Springer 2022.

<div style="font-size: 1em; font-weight: bold; text-align: center; margin-bottom: 20px;">
"Humanity is just a passing phase in the evolution of intelligence." — Geoffrey Hinton
</div>

<style>
    #scrambledText {
  font-size: 1.0rem; /* Normal text size */
  cursor: pointer;
  color: var(--global-text-color); /* Default text color */
  transition: color 0.3s ease-in-out;
  white-space: nowrap; /* Prevent line breaks */
  overflow: hidden; /* Hides extra text during the animation */
    }
    
      #scrambledText:hover {
      color: var(--global-hover-color); /* Text color on hover */
    }
</style>

<script>
  document.addEventListener("DOMContentLoaded", () => {
    const scrambledTextElement = document.getElementById("scrambledText");
    const unscrambledText = "Hi, welcome fellow human!";
    const scrambledText = scrambledTextElement.textContent;

    let isUnscrambled = false;

    scrambledTextElement.addEventListener("click", () => {
      if (isUnscrambled) return; 

      isUnscrambled = true; 
      const duration = 2000; 
      const interval = 50; 
      let progress = 0;

      const animateUnscramble = setInterval(() => {
        progress += interval;
        const percentage = progress / duration;
        const revealLength = Math.floor(percentage * unscrambledText.length);

        // Gradually replace scrambled text with correct letters
        scrambledTextElement.textContent =
          unscrambledText.slice(0, revealLength) +
          scrambledText.slice(revealLength);

        if (progress >= duration) {
          clearInterval(animateUnscramble); 
          scrambledTextElement.textContent = unscrambledText; 
          scrambledTextElement.style.cursor = "default"; 
        }
      }, interval);
    });
  });
</script>