## CSS
body {
  text-align: center;
  font-family: Arial, sans-serif;
  background: #f0f0f0;
}
#game-area {
  width: 300px;
  height: 300px;
  border: 2px solid #333;
  margin: 20px auto;
  position: relative;
  background: white;
}
#square {
  width: 50px;
  height: 50px;
  background: blue;
  position: absolute;
  top: 0;
  left: 0;
  cursor: pointer;
}
button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

## JavaScript
const square = document.getElementById('square');
const scoreDisplay = document.getElementById('score');
const timeDisplay = document.getElementById('time');
const startBtn = document.getElementById('start-btn');
let score = 0;
let time = 30;
let gameInterval, timerInterval;
function moveSquare() {
  const area = document.getElementById('game-area');
  const maxX = area.clientWidth - square.clientWidth;
  const maxY = area.clientHeight - square.clientHeight;
  const x = Math.floor(Math.random() * maxX);
  const y = Math.floor(Math.random() * maxY);
  square.style.left = x + 'px';
  square.style.top = y + 'px';
}
square.addEventListener('click', () => {
  if (time > 0) {
    score++;
    scoreDisplay.textContent = score;
    moveSquare();
  }
});
startBtn.addEventListener('click', () => {
  score = 0;
  time = 30;
  scoreDisplay.textContent = score;
  timeDisplay.textContent = time;

  gameInterval = setInterval(moveSquare, 800);

  timerInterval = setInterval(() => {
    time--;
    timeDisplay.textContent = time;
    if (time <= 0) {
      clearInterval(gameInterval);
      clearInterval(timerInterval);
      alert('Fim de jogo! Pontuação final: ' + score);
    }
  }, 1000);
});

