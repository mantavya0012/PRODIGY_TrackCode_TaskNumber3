# PRODIGY_TrackCode_TaskNumber3
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #ffecd2, #fcb69f);
    }

    .game-container {
      background: rgba(255, 255, 255, 0.2);
      backdrop-filter: blur(10px);
      padding: 20px;
      border-radius: 20px;
      text-align: center;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
    }

    h1 {
      color: #fff;
      margin-bottom: 20px;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 10px;
      justify-content: center;
      margin-bottom: 20px;
    }

    .cell {
      width: 100px;
      height: 100px;
      background: #fff;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2rem;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.3s;
    }

    .cell:hover {
      background: #f0f0f0;
    }

    .status {
      color: #fff;
      font-size: 1.2rem;
      margin-bottom: 15px;
    }

    button {
      padding: 10px 20px;
      background: #fff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      transition: transform 0.2s ease, background 0.3s ease;
    }

    button:hover {
      background: #f0f0f0;
      transform: translateY(-2px);
    }
  </style>
</head>
<body>
  <div class="game-container">
    <h1>Tic Tac Toe</h1>
    <div class="status" id="status">Player X's turn</div>
    <div class="board" id="board"></div>
    <button onclick="resetGame()">Restart Game</button>
  </div>

  <script>
    const boardElement = document.getElementById('board');
    const statusElement = document.getElementById('status');
    let board = Array(9).fill(null);
    let currentPlayer = 'X';
    let gameActive = true;

    function createBoard() {
      boardElement.innerHTML = '';
      board.forEach((cell, index) => {
        const cellElement = document.createElement('div');
        cellElement.classList.add('cell');
        cellElement.textContent = cell;
        cellElement.addEventListener('click', () => handleCellClick(index));
        boardElement.appendChild(cellElement);
      });
    }

    function handleCellClick(index) {
      if (board[index] || !gameActive) return;
      board[index] = currentPlayer;
      checkWinner();
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      updateStatus();
      createBoard();
    }

    function checkWinner() {
      const winningCombos = [
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
      ];

      for (const combo of winningCombos) {
        const [a,b,c] = combo;
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          statusElement.textContent = `Player ${board[a]} wins!`;
          gameActive = false;
          return;
        }
      }

      if (!board.includes(null)) {
        statusElement.textContent = "It's a draw!";
        gameActive = false;
      }
    }

    function updateStatus() {
      if (gameActive) {
        statusElement.textContent = `Player ${currentPlayer}'s turn`;
      }
    }

    function resetGame() {
      board = Array(9).fill(null);
      currentPlayer = 'X';
      gameActive = true;
      updateStatus();
      createBoard();
    }

    createBoard();
  </script>
</body>
</html>
