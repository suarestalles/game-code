## CSS
body { /* Estilo geral da página */
  text-align: center; /* Centraliza o texto */
  font-family: Arial, sans-serif; /* Define a fonte */
  background: #f0f0f0; /* Fundo cinza claro */
}
#game-area { /* Área do jogo */
  width: 300px; /* Largura da área */
  height: 300px; /* Altura da área */
  border: 2px solid #333; /* Borda preta */
  margin: 20px auto; /* Centraliza horizontalmente e dá espaço em cima */
  position: relative; /* Necessário para posicionar o quadrado dentro */
  background: white; /* Fundo branco */
}
#square { /* Quadrado azul clicável */
  width: 50px; /* Largura */
  height: 50px; /* Altura */
  background: blue; /* Cor de fundo azul */
  position: absolute; /* Permite mover com left e top */
  top: 0; /* Começa no topo */
  left: 0; /* Começa na esquerda */
  cursor: pointer; /* Muda o cursor para “mãozinha” */
}
button { /* Estilo do botão */
  padding: 10px 20px; /* Espaçamento interno */
  font-size: 16px; /* Tamanho da fonte */
  cursor: pointer; /* Mãozinha ao passar por cima */
}

## JavaScript
const square = document.getElementById('square'); // Pega o elemento do quadrado pelo ID
const scoreDisplay = document.getElementById('score'); // Pega o elemento que mostra a pontuação
const timeDisplay = document.getElementById('time'); // Pega o elemento que mostra o tempo
const startBtn = document.getElementById('start-btn'); // Pega o botão de iniciar
let score = 0; // Pontuação inicial
let time = 30; // Tempo inicial (30 segundos)
let gameInterval, timerInterval; // Variáveis para guardar os intervalos (movimento e cronômetro)
function moveSquare() { // Função para mover o quadrado aleatoriamente
  const area = document.getElementById('game-area'); // Pega a área do jogo
  const maxX = area.clientWidth - square.clientWidth; // Calcula o limite máximo no eixo X
  const maxY = area.clientHeight - square.clientHeight; // Calcula o limite máximo no eixo Y
  const x = Math.floor(Math.random() * maxX); // Gera posição X aleatória
  const y = Math.floor(Math.random() * maxY); // Gera posição Y aleatória
  square.style.left = x + 'px'; // Atualiza a posição horizontal
  square.style.top = y + 'px'; // Atualiza a posição vertical
}
square.addEventListener('click', () => { // Quando o quadrado for clicado
  if (time > 0) { // Verifica se o tempo ainda não acabou
    score++; // Aumenta a pontuação
    scoreDisplay.textContent = score; // Atualiza o placar na tela
    moveSquare(); // Move o quadrado para outra posição
  }
});
startBtn.addEventListener('click', () => { // Quando clicar no botão de iniciar
  score = 0; // Reseta a pontuação
  time = 30; // Reseta o tempo
  scoreDisplay.textContent = score; // Atualiza placar para 0
  timeDisplay.textContent = time; // Atualiza o cronômetro para 30

  gameInterval = setInterval(moveSquare, 800); // Move o quadrado a cada 800ms automaticamente

  timerInterval = setInterval(() => { // Inicia o cronômetro
    time--; // Diminui 1 segundo
    timeDisplay.textContent = time; // Atualiza o tempo na tela
    if (time <= 0) { // Se o tempo acabou
      clearInterval(gameInterval); // Para o movimento do quadrado
      clearInterval(timerInterval); // Para o cronômetro
      alert('Fim de jogo! Pontuação final: ' + score); // Mostra alerta com a pontuação final
    }
  }, 1000); // Intervalo de 1 segundo
});





