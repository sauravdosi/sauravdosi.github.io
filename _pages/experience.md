---
layout: page
permalink: /experience/
title: experience
description: Walk through my career journey, from solving real-world puzzles to crafting innovative solutions that matter. 💼🚀
nav: true
nav_order: 3
---

<div class="container mt-5">
  <h1 class="text-center mb-4">career timeline</h1>
  <div class="timeline position-relative">

    <!-- Example Timeline Item (Reusable Structure) -->
    {% assign experiences = site.data.timeline_experiences %}
    {% for experience in experiences %}
    <div class="timeline-item d-flex flex-row align-items-center mb-5">
      <!-- Timeline Marker -->
      <div class="marker bg-primary rounded-circle position-absolute shadow-sm" 
           style="left: 50%; transform: translate(-50%, -50%); width: 30px; height: 30px;"></div>
        
        
        {% assign remainder = forloop.index | modulo: 2 %}

      <div class="content bg-light p-4 rounded shadow-sm position-relative 
    {% if remainder == 0 %} mr-auto {% else %} ml-auto {% endif %}" 
    style="max-width: 44%;">
        <h2 class="position-title">{{ experience.title }}</h2>
        <h4 class="company-name text-muted">{{ experience.company }}</h4>
        <p class="date text-muted">{{ experience.date }}</p>
          {% for point in experience.points %}
          <li>{{ point }}</li>
          {% endfor %}
        <div class="badge-container">
          {% for tech in experience.tech_stack %}
          <span class="badge bg-primary text-white">{{ tech }}</span>
          {% endfor %}
        </div>
      </div>
    </div>
    {% endfor %}

  </div>
</div>

<script>
 
</script>

<style>
  /* Basic Styles */
  .timeline {
    position: relative;
    padding: 20px 0;
  }

  .timeline-item {
    display: flex;
    justify-content: space-between;
  }

  .timeline-item .icon {
    width: 100px;
    height: 100px;
    display: flex !important;
    justify-content: center !important;
    align-items: center !important;
    background-color: var(--global-bg-color) !important;
    border-radius: 50%;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .timeline-item .content {
    background-color: var(--global-card-bg-color) !important;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

.timeline-item .marker {
  z-index: 1;
  border: 4px solid var(--global-bg-color);
background-color: var(--global-theme-color) !important;
}

  .timeline-item .content h2 {
    font-size: 1.5rem;
  }

  .timeline-item .content h4 {
    font-size: 1.2rem;
  }

  .timeline:before {
    content: '';
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 4px;
    height: 100%;
    background-color: var(--global-theme-color);
    z-index: 0;
  }

  /* Responsive Layout */
@media (max-width: 768px) {
  /* Move timeline to the extreme left */
  .timeline {
    padding-left: 20px; /* Ensure proper spacing from the screen edge */
  }

  .timeline:before {
    left: 0;
  }

  .timeline .marker {
    left: 0 !important; /* Keep the marker aligned to the timeline */
  }

  /* Align content to the right of the timeline */
  .timeline-item {
    flex-direction: row;
    align-items: flex-start;
  }

  .timeline .content {
    max-width: 100% !important;
    width: 100% !important;
    margin-left: 30px !important; /* Space between the content and the timeline */
  }
}

.badge-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: left;
  gap: 5px;
  max-width: 1000px;
  margin: 10px auto 0 auto;
}

  /* Tech Stack Badges */
  .badge-container .badge {
    background-color: var(--global-theme-color) !important; /* Change this to match your theme */
  color: var(--global-text-color);
  padding: 5px 10px;
  border-radius: 25px;
  font-size: 0.9rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

.badge:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
</style>
