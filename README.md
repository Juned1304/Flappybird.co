<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Motorcycle Dodge Game</title>
  <style>
    body {
      margin: 0;
      background-color: #333;
      overflow: hidden;
    }
    canvas {
      display: block;
      margin: auto;
      background-color: #444;
    }
  </style>
</head>
<body>
<canvas id="gameCanvas" width="400" height="600"></canvas>
<script>
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

const WIDTH = 400, HEIGHT = 600;
let bike = { x: WIDTH / 2 - 20, y: HEIGHT - 100, w: 40, h: 60 };
const bikeSpeed = 5;

let cars = [];
let carTimer = 0;
const carWidth = 40, carHeight = 60;

let lines = [];
for (let i = 0; i < HEIGHT; i += 80) {
  lines.push({ x: WIDTH / 2 - 5, y: i, w: 10, h: 40 });
}

let score = 0;
let gameActive = true;
let keys = {};

function drawRect(obj, color) {
  ctx.fillStyle = color;
  ctx.fillRect(obj.x, obj.y, obj.w, obj.h);
}

function drawText(text, x, y, size = 24) {
  ctx.fillStyle = "white";
  ctx.font = `${size}px Arial`;
  ctx.fillText(text, x, y);
}

function resetGame() {
  bike.x = WIDTH / 2 - 20;
  cars = [];
  score = 0;
  gameActive = true;
}

document.addEventListener("keydown", (e) => {
  keys[e.key] = true;
  if (!gameActive && e.code === "Space") {
    resetGame();
  }
});
document.addEventListener("keyup", (e) => {
  keys[e.key] = false;
});

function gameLoop() {
  ctx.clearRect(0, 0, WIDTH, HEIGHT);
  ctx.fillStyle = "#444";
  ctx.fillRect(0, 0, WIDTH, HEIGHT);

  if (gameActive) {
    // Move bike
    if (keys["ArrowLeft"] && bike.x > 80) bike.x -= bikeSpeed;
    if (keys["ArrowRight"] && bike.x + bike.w < 320) bike.x += bikeSpeed;

    // Spawn cars
    if (carTimer <= 0) {
      let positions = [100, 150, 200, 250];
      let x = positions[Math.floor(Math.random() * positions.length)];
      cars.push({ x: x, y: -carHeight, w: carWidth, h: carHeight });
      carTimer = 60;
    } else {
      carTimer--;
    }

    // Move and draw cars
    for (let car of cars) {
      car.y += 5;
      drawRect(car, "red");

      if (
        car.x < bike.x + bike.w &&
        car.x + car.w > bike.x &&
        car.y < bike.y + bike.h &&
        car.y + car.h > bike.y
      ) {
        gameActive = false;
      }
    }
    cars = cars.filter(car => car.y < HEIGHT);

    // Road lines
    for (let line of lines) {
      line.y += 5;
      if (line.y > HEIGHT) line.y = -40;
      drawRect(line, "white");
    }

    // Draw bike
    drawRect(bike, "yellow");

    // Score
    score += 0.1;
    drawText("Score: " + Math.floor(score), 10, 30);
  } else {
    drawText("Game Over - Press Space", 70, HEIGHT / 2);
  }

  requestAnimationFrame(gameLoop);
}

gameLoop();
</script>
</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Motorcycle Dodge Game</title>
  <style>
    body {
      margin: 0;
      background-color: #333;
      overflow: hidden;
    }
    canvas {
      display: block;
      margin: auto;
      background-color: #444;
    }
  </style>
</head>
<body>
<canvas id="gameCanvas" width="400" height="600"></canvas>
<script>
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

const WIDTH = 400, HEIGHT = 600;
let bike = { x: WIDTH / 2 - 20, y: HEIGHT - 100, w: 40, h: 60 };
const bikeSpeed = 5;

let cars = [];
let carTimer = 0;
const carWidth = 40, carHeight = 60;

let lines = [];
for (let i = 0; i < HEIGHT; i += 80) {
  lines.push({ x: WIDTH / 2 - 5, y: i, w: 10, h: 40 });
}

let score = 0;
let gameActive = true;
let keys = {};

function drawRect(obj, color) {
  ctx.fillStyle = color;
  ctx.fillRect(obj.x, obj.y, obj.w, obj.h);
}

function drawText(text, x, y, size = 24) {
  ctx.fillStyle = "white";
  ctx.font = `${size}px Arial`;
  ctx.fillText(text, x, y);
}

function resetGame() {
  bike.x = WIDTH / 2 - 20;
  cars = [];
  score = 0;
  gameActive = true;
}

document.addEventListener("keydown", (e) => {
  keys[e.key] = true;
  if (!gameActive && e.code === "Space") {
    resetGame();
  }
});
document.addEventListener("keyup", (e) => {
  keys[e.key] = false;
});

function gameLoop() {
  ctx.clearRect(0, 0, WIDTH, HEIGHT);
  ctx.fillStyle = "#444";
  ctx.fillRect(0, 0, WIDTH, HEIGHT);

  if (gameActive) {
    // Move bike
    if (keys["ArrowLeft"] && bike.x > 80) bike.x -= bikeSpeed;
    if (keys["ArrowRight"] && bike.x + bike.w < 320) bike.x += bikeSpeed;

    // Spawn cars
    if (carTimer <= 0) {
      let positions = [100, 150, 200, 250];
      let x = positions[Math.floor(Math.random() * positions.length)];
      cars.push({ x: x, y: -carHeight, w: carWidth, h: carHeight });
      carTimer = 60;
    } else {
      carTimer--;
    }

    // Move and draw cars
    for (let car of cars) {
      car.y += 5;
      drawRect(car, "red");

      if (
        car.x < bike.x + bike.w &&
        car.x + car.w > bike.x &&
        car.y < bike.y + bike.h &&
        car.y + car.h > bike.y
      ) {
        gameActive = false;
      }
    }
    cars = cars.filter(car => car.y < HEIGHT);

    // Road lines
    for (let line of lines) {
      line.y += 5;
      if (line.y > HEIGHT) line.y = -40;
      drawRect(line, "white");
    }

    // Draw bike
    drawRect(bike, "yellow");

    // Score
    score += 0.1;
    drawText("Score: " + Math.floor(score), 10, 30);
  } else {
    drawText("Game Over - Press Space", 70, HEIGHT / 2);
  }

  requestAnimationFrame(gameLoop);
}

gameLoop();
</script>
</body>
</html>
