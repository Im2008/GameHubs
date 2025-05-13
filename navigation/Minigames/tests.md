---
layout: bootstrap
title: Tests
description: Tests
permalink: /tests
Author: Ian
---

<div class="container text-center p-5">
  <h1 class="text-success mb-4">🧪 Brain Games</h1>
  <p class="text-muted mb-5">Select a game to test your mental skills.</p>

  <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
    <div class="col">
      <a href="{{site.baseurl}}/aim" class="text-decoration-none">
        <div class="card game-card h-100 p-4 text-start">
          <h4 class="text-success">🎯 Aim Trainer</h4>
          <p class="text-light">Test how quickly and accurately you can click targets.</p>
        </div>
      </a>
    </div>
    <div class="col">
      <a href="{{site.baseurl}}/number" class="text-decoration-none">
        <div class="card game-card h-100 p-4 text-start">
          <h4 class="text-success">🔢 Number Memory</h4>
          <p class="text-light">Remember and repeat numbers that get longer each round.</p>
        </div>
      </a>
    </div>
    <div class="col">
      <a href="{{site.baseurl}}/reaction" class="text-decoration-none">
        <div class="card game-card h-100 p-4 text-start">
          <h4 class="text-success">⚡ Reaction Time</h4>
          <p class="text-light">Measure how fast you can respond to visual signals.</p>
        </div>
      </a>
    </div>
    <div class="col">
      <a href="{{site.baseurl}}/sequence" class="text-decoration-none">
        <div class="card game-card h-100 p-4 text-start">
          <h4 class="text-success">🔁 Sequence Memory</h4>
          <p class="text-light">Repeat the visual sequence as it grows longer each round.</p>
        </div>
      </a>
    </div>
    <div class="col">
      <a href="{{site.baseurl}}/typing" class="text-decoration-none">
        <div class="card game-card h-100 p-4 text-start">
          <h4 class="text-success">⌨️ Typing Test</h4>
          <p class="text-light">Type a sentence as fast and accurately as possible.</p>
        </div>
      </a>
    </div>
  </div>
</div>

<style>
  .game-card {
    background-color: #161b22;
    border: 1px solid #30363d;
    border-radius: 1rem;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .game-card:hover {
    transform: scale(1.03);
    box-shadow: 0 0 20px rgba(0,255,0,0.1);
    border-color: #2ea043;
  }

  .game-card h4 {
    margin-bottom: 0.5rem;
  }

  .game-card p {
    margin-bottom: 0;
  }
</style>
