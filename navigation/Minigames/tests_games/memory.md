---
layout: bootstrap
title: Visual Memory
description: Visual Memory Game
permalink: /memory
Author: Zach
---

<div class="container text-center p-5">
  <h1 class="mb-4 text-success">🧠 Visual Memory Test</h1>

  <div class="card game-card p-4 mx-auto" style="max-width: 500px;">
    <div id="grid" class="d-grid mx-auto mb-4" style="grid-template-columns: repeat(3, 80px); grid-gap: 10px;"></div>
    <button id="startMemoryBtn" class="btn btn-success">Start</button>
    <p class="mt-3 score" id="memoryStats"></p>
  </div>

  <p class="mt-4 text-muted">Click all the squares that appeared. Progress to harder levels as you succeed!</p>
</div>

<style>
  .game-card {
    background-color: #161b22;
    border: none;
    border-radius: 1rem;
    box-shadow: 0 0 20px rgba(0,255,0,0.1);
  }

  #grid button {
    width: 80px;
    height: 80px;
    border-radius: 0.5rem;
    background-color: #21262d;
    border: 2px solid #30363d;
    transition: background-color 0.2s;
  }

  #grid button.active {
    background-color: #2ea043;
  }

  #grid button:disabled {
    cursor: default;
  }
</style>

<script>
  const grid = document.getElementById('grid');
  const startBtn = document.getElementById('startMemoryBtn');
  const stats = document.getElementById('memoryStats');

  let activeCells = [];
  let userSelections = [];
  let level = 1;
  let gridSize = 3;
  let winStreak = 0;

  function createGrid() {
    grid.innerHTML = '';
    const totalCells = gridSize * gridSize;
    grid.style.gridTemplateColumns = `repeat(${gridSize}, 80px)`;
    for (let i = 0; i < totalCells; i++) {
      const btn = document.createElement('button');
      btn.disabled = true;
      btn.dataset.index = i;
      btn.addEventListener('click', () => handleUserInput(i));
      grid.appendChild(btn);
    }
  }

  function flashCells() {
    const totalFlashes = Math.floor((gridSize * gridSize) / 2); // Half of the squares appear
    activeCells = [];
    while (activeCells.length < totalFlashes) {
      const randomIndex = Math.floor(Math.random() * (gridSize * gridSize));
      if (!activeCells.includes(randomIndex)) {
        activeCells.push(randomIndex);
      }
    }
    activeCells.forEach(index => {
      const cell = grid.children[index];
      cell.classList.add('active');
      setTimeout(() => cell.classList.remove('active'), gridSize * 1000); // Increase time based on grid size
    });
    setTimeout(() => {
      Array.from(grid.children).forEach(cell => (cell.disabled = false));
    }, gridSize * 1000 + 200); // Adjust delay for user interaction
  }

  function handleUserInput(index) {
    if (userSelections.includes(index)) {
      stats.innerHTML = `❌ You clicked the same square twice! You lost at level <strong>${level}</strong>.`;
      resetGame();
      return;
    }

    if (activeCells.includes(index)) {
      userSelections.push(index);
      if (userSelections.length === activeCells.length) {
        winStreak++;
        if (winStreak === 3) {
          gridSize++;
          winStreak = 0;
          stats.textContent = `🎉 Advanced to ${gridSize}x${gridSize} grid!`;
        }
        setTimeout(nextRound, 800);
      }
    } else {
      stats.innerHTML = `❌ You lost at level <strong>${level}</strong>.`;
      resetGame();
    }
  }

  function nextRound() {
    level++;
    userSelections = [];
    createGrid();
    flashCells();
    stats.textContent = `🟢 Level ${level}`;
  }

  function resetGame() {
    activeCells = [];
    userSelections = [];
    level = 1;
    gridSize = 3;
    winStreak = 0;
    startBtn.textContent = "Try Again";
    Array.from(grid.children).forEach(cell => (cell.disabled = true));
  }

  startBtn.addEventListener('click', () => {
    resetGame();
    createGrid();
    setTimeout(() => {
      flashCells();
      stats.textContent = `🟢 Level ${level}`;
      startBtn.textContent = "Restart";
    }, 1000);
  });

  function getRandomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }

  // Disable copy/paste functionality
  document.addEventListener('copy', (e) => e.preventDefault());
  document.addEventListener('paste', (e) => e.preventDefault());
</script>

<script>
// --- Background Music ---
const music = new Audio('{{site.baseurl}}/assets/audio/22dksummit.mp3');
music.loop = true;
music.volume = 0.5;

// Play music after first user interaction (required by browsers)
function startMusicOnce() {
  music.play().catch(() => {});
  window.removeEventListener('click', startMusicOnce);
  window.removeEventListener('keydown', startMusicOnce);
}
window.addEventListener('click', startMusicOnce);
window.addEventListener('keydown', startMusicOnce);
</script>