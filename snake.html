
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Snake — After Hours</title>
<style>
:root {
  font-family: system-ui, sans-serif;
  color: #eff5f3;
  background: #080d12;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 20px;
}
.game { width: min(100%, 600px); }
.topline, .brand, .scores, .gamebar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
}
.topline { margin-bottom: 20px; }
h1 { font-size: 1.2rem; margin: 0; }
p { color: #86938f; }
.scores { gap: 20px; text-align: right; }
.score { color: #7ef4c2; font-size: 1.2rem; }
.board {
  position: relative;
  padding: 8px;
  border: 1px solid #263638;
  border-radius: 16px;
  background: #11191e;
}
canvas {
  display: block;
  width: 100%;
  height: auto;
  border-radius: 10px;
  background: #0b1217;
}
.overlay {
  position: absolute;
  inset: 8px;
  display: grid;
  place-items: center;
  padding: 20px;
  text-align: center;
  background: #080d12d9;
  border-radius: 10px;
}
.overlay[hidden] { display: none; }
button {
  cursor: pointer;
  border: 1px solid #344541;
  border-radius: 10px;
  padding: 11px 16px;
  background: #15211f;
  color: white;
  font: inherit;
}
.primary {
  background: #7ef4c2;
  color: #08130e;
  font-weight: bold;
}
.gamebar { margin-top: 12px; }
.touch {
  display: grid;
  grid-template-columns: repeat(3, 54px);
  grid-template-rows: repeat(2, 44px);
  justify-content: center;
  gap: 6px;
  margin-top: 18px;
}
.touch button { padding: 5px; }
.up { grid-area: 1 / 2; }
.left { grid-area: 2 / 1; }
.down { grid-area: 2 / 2; }
.right { grid-area: 2 / 3; }
.hint { text-align: center; font-size: .8rem; }
@media (min-width: 700px) and (pointer: fine) {
  .touch { display: none; }
}
</style>
</head>
<body>
<main class="game">
  <header class="topline">
    <div class="brand">
      <span style="color:#7ef4c2;font-size:28px">〰</span>
      <div>
        <h1>After Hours</h1>
        <small style="color:#86938f">A little classic</small>
      </div>
    </div>
    <div class="scores">
      <div>Score<br><span class="score" id="score">00</span></div>
      <div>Best<br><span class="score" id="best">00</span></div>
    </div>
  </header>

  <section class="board">
    <canvas id="canvas" width="576" height="432"></canvas>
    <div class="overlay" id="overlay">
      <div>
        <h2 id="overlayTitle">Ready when you are</h2>
        <p id="overlayMessage">Eat the food. Avoid the walls and yourself!</p>
        <button class="primary" id="start">Start game</button>
      </div>
    </div>
  </section>

  <div class="gamebar">
    <span id="status">Ready to play</span>
    <span>Level <span id="level">01</span></span>
    <button id="pause" hidden>Pause</button>
  </div>

  <div class="touch">
    <button class="up" data-dir="up">▲</button>
    <button class="left" data-dir="left">◀</button>
    <button class="down" data-dir="down">▼</button>
    <button class="right" data-dir="right">▶</button>
  </div>

  <p class="hint">Arrow keys / WASD to move · Space to pause</p>
</main>

<script>
(() => {
  const canvas = document.getElementById("canvas");
  const ctx = canvas.getContext("2d");
  const overlay = document.getElementById("overlay");
  const startBtn = document.getElementById("start");
  const pauseBtn = document.getElementById("pause");
  const scoreEl = document.getElementById("score");
  const bestEl = document.getElementById("best");
  const levelEl = document.getElementById("level");
  const statusEl = document.getElementById("status");
  const titleEl = document.getElementById("overlayTitle");
  const messageEl = document.getElementById("overlayMessage");

  const cols = 24, rows = 18, cell = 24;
  let snake, food, dir, nextDir, score = 0, level = 1;
  let state = "ready", timer = null, best = 0;

  try {
    best = Number(localStorage.getItem("snakeBest")) || 0;
  } catch (_) {}

  const directions = {
    up: { x: 0, y: -1 },
    down: { x: 0, y: 1 },
    left: { x: -1, y: 0 },
    right: { x: 1, y: 0 }
  };

  function updateScore() {
    scoreEl.textContent = String(score).padStart(2, "0");
    bestEl.textContent = String(best).padStart(2, "0");
    levelEl.textContent = String(level).padStart(2, "0");
  }

  function placeFood() {
    const empty = [];
    for (let y = 0; y < rows; y++) {
      for (let x = 0; x < cols; x++) {
        if (!snake.some(s => s.x === x && s.y === y)) {
          empty.push({ x, y });
        }
      }
    }
    if (!empty.length) {
      endGame(true);
      return;
    }
    food = empty[Math.floor(Math.random() * empty.length)];
  }

  function reset() {
    snake = [
      { x: 11, y: 9 },
      { x: 10, y: 9 },
      { x: 9, y: 9 }
    ];
    dir = { x: 1, y: 0 };
    nextDir = { ...dir };
    score = 0;
    level = 1;
    placeFood();
    updateScore();
    draw();
  }

  function roundedRect(x, y, w, h, r) {
    ctx.beginPath();
    ctx.roundRect(x, y, w, h, r);
    ctx.fill();
  }

  function draw() {
    ctx.fillStyle = "#0b1217";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.strokeStyle = "rgba(170,205,195,.06)";
    ctx.beginPath();
    for (let x = 24; x < canvas.width; x += cell) {
      ctx.moveTo(x, 0);
      ctx.lineTo(x, canvas.height);
    }
    for (let y = 24; y < canvas.height; y += cell) {
      ctx.moveTo(0, y);
      ctx.lineTo(canvas.width, y);
    }
    ctx.stroke();

    if (food) {
      ctx.fillStyle = "#ff6688";
      ctx.beginPath();
      ctx.arc(
        (food.x + .5) * cell,
        (food.y + .5) * cell,
        7, 0, Math.PI * 2
      );
      ctx.fill();
    }

    snake.forEach((s, i) => {
      ctx.fillStyle = i === 0
        ? "#b2ffdb"
        : `hsl(153 65% ${Math.max(35, 60 - i * .6)}%)`;
      roundedRect(s.x * cell + 2, s.y * cell + 2, 20, 20, 5);

      if (i === 0) {
        ctx.fillStyle = "#123129";
        ctx.beginPath();
        ctx.arc(
          s.x * cell + 9 + dir.x * 4,
          s.y * cell + 9 + dir.y * 4,
          2, 0, Math.PI * 2
        );
        ctx.arc(
          s.x * cell + 15 + dir.x * 4,
          s.y * cell + 15 + dir.y * 4,
          2, 0, Math.PI * 2
        );
        ctx.fill();
      }
    });
  }

  function startGame() {
    clearTimeout(timer);
    reset();
    state = "running";
    statusEl.textContent = "In the zone";
    pauseBtn.hidden = false;
    pauseBtn.textContent = "Pause";
    overlay.hidden = true;
    timer = setTimeout(tick, getDelay());
  }

  function getDelay() {
    return Math.max(72, 155 - (level - 1) * 10);
  }

  function tick() {
    if (state !== "running") return;

    dir = nextDir;
    const head = {
      x: snake[0].x + dir.x,
      y: snake[0].y + dir.y
    };
    const ate = head.x === food.x && head.y === food.y;
    const body = ate ? snake : snake.slice(0, -1);

    const wallHit =
      head.x < 0 || head.x >= cols ||
      head.y < 0 || head.y >= rows;
    const bodyHit = body.some(
      s => s.x === head.x && s.y === head.y
    );

    if (wallHit || bodyHit) {
      endGame(false);
      return;
    }

    snake.unshift(head);

    if (ate) {
      score += 10;
      best = Math.max(best, score);
      level = Math.floor(score / 50) + 1;

      try {
        localStorage.setItem("snakeBest", String(best));
      } catch (_) {}

      updateScore();
      placeFood();
      if (state !== "running") return;
    } else {
      snake.pop();
    }

    draw();
    timer = setTimeout(tick, getDelay());
  }

  function endGame(won) {
    clearTimeout(timer);
    state = "gameover";
    statusEl.textContent = won ? "Board cleared" : "Game over";
    pauseBtn.hidden = true;
    titleEl.textContent = won ? "You won!" : "Nice run!";
    messageEl.textContent = `Your final score: ${score}`;
    startBtn.textContent = "Play again";
    overlay.hidden = false;
  }

  function togglePause() {
    if (state === "running") {
      clearTimeout(timer);
      state = "paused";
      statusEl.textContent = "Paused";
      pauseBtn.textContent = "Resume";
      titleEl.textContent = "Take your time.";
      messageEl.textContent = "Your game is paused.";
      startBtn.textContent = "Keep playing";
      overlay.hidden = false;
    } else if (state === "paused") {
      state = "running";
      statusEl.textContent = "In the zone";
      pauseBtn.textContent = "Pause";
      overlay.hidden = true;
      timer = setTimeout(tick, getDelay());
    }
  }

  function changeDirection(name) {
    if (state !== "running") return;
    const d = directions[name];
    if (!d) return;
    if (d.x === -dir.x && d.y === -dir.y) return;
    nextDir = d;
  }

  document.addEventListener("keydown", event => {
    const keyMap = {
      ArrowUp: "up", KeyW: "up",
      ArrowDown: "down", KeyS: "down",
      ArrowLeft: "left", KeyA: "left",
      ArrowRight: "right", KeyD: "right"
    };

    if (event.code === "Space") {
      event.preventDefault();
      if (state === "ready" || state === "gameover") {
        startGame();
      } else {
        togglePause();
      }
      return;
    }

    if (keyMap[event.code]) {
      event.preventDefault();
      changeDirection(keyMap[event.code]);
    }
  });

  startBtn.addEventListener("click", () => {
    if (state === "paused") {
      togglePause();
    } else {
      startGame();
    }
  });

  pauseBtn.addEventListener("click", togglePause);

  document.querySelectorAll("[data-dir]").forEach(button => {
    button.addEventListener("click", () => {
      if (state === "ready" || state === "gameover") {
        startGame();
      }
      changeDirection(button.dataset.dir);
    });
  });

  reset();
})();
</script>
</body>
</html>
