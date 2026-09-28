# game-bot-w.a-
game by sarnur 
index.httml

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Bot WA - Tic Tac Toe</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background-color: #121212;
            color: #ffffff;
            margin: 0;
            padding: 20px;
        }
        h1 {
            color: #25D366; /* Warna khas WhatsApp */
            margin-bottom: 10px;
        }
        .status {
            font-size: 1.2rem;
            margin-bottom: 20px;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 90px);
            grid-template-rows: repeat(3, 90px);
            gap: 10px;
        }
        .cell {
            background-color: #1e1e1e;
            border: 2px solid #25D366;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            font-weight: bold;
            cursor: pointer;
            user-select: none;
            transition: background 0.2s;
        }
        .cell:hover {
            background-color: #2a2a2a;
        }
        .cell.x {
            color: #ff4757;
        }
        .cell.o {
            color: #1e90ff;
        }
        button {
            margin-top: 25px;
            padding: 10px 20px;
            font-size: 1rem;
            font-weight: bold;
            color: #ffffff;
            background-color: #25D366;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: 0.2s;
        }
        button:hover {
            background-color: #1da851;
        }
    </style>
</head>
<body>

    <h1>Tic Tac Toe</h1>
    <div class="status" id="status">Giliran Player: <b style="color:#ff4757;">X</b></div>

    <div class="board" id="board">
        <div class="cell" data-index="0"></div>
        <div class="cell" data-index="1"></div>
        <div class="cell" data-index="2"></div>
        <div class="cell" data-index="3"></div>
        <div class="cell" data-index="4"></div>
        <div class="cell" data-index="5"></div>
        <div class="cell" data-index="6"></div>
        <div class="cell" data-index="7"></div>
        <div class="cell" data-index="8"></div>
    </div>

    <button onclick="resetGame()">Main Lagi</button>

    <script>
        let boardState = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let isGameActive = true;

        const statusDisplay = document.getElementById("status");
        const cells = document.querySelectorAll(".cell");

        const winningConditions = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8], // Baris
            [0, 3, 6], [1, 4, 7], [2, 5, 8], // Kolom
            [0, 4, 8], [2, 4, 6]             // Diagonal
        ];

        cells.forEach(cell => {
            cell.addEventListener("click", handleCellClick);
        });

        function handleCellClick(e) {
            const clickedCell = e.target;
            const clickedIndex = parseInt(clickedCell.getAttribute("data-index"));

            if (boardState[clickedIndex] !== "" || !isGameActive) {
                return;
            }

            boardState[clickedIndex] = currentPlayer;
            clickedCell.innerText = currentPlayer;
            clickedCell.classList.add(currentPlayer.toLowerCase());

            checkResult();
        }

        function checkResult() {
            let roundWon = false;

            for (let i = 0; i < winningConditions.length; i++) {
                const [a, b, c] = winningConditions[i];
                if (boardState[a] === "" || boardState[b] === "" || boardState[c] === "") {
                    continue;
                }
                if (boardState[a] === boardState[b] && boardState[b] === boardState[c]) {
                    roundWon = true;
                    break;
                }
            }

            if (roundWon) {
                statusDisplay.innerHTML = `Pemain <b style="color:${currentPlayer === 'X' ? '#ff4757' : '#1e90ff'}">${currentPlayer}</b> Menang! 🎉`;
                isGameActive = false;
                return;
            }

            if (!boardState.includes("")) {
                statusDisplay.innerText = "Hasil Seri! 🤝";
                isGameActive = false;
                return;
            }

            currentPlayer = currentPlayer === "X" ? "O" : "X";
            statusDisplay.innerHTML = `Giliran Player: <b style="color:${currentPlayer === 'X' ? '#ff4757' : '#1e90ff'}">${currentPlayer}</b>`;
        }

        function resetGame() {
            boardState = ["", "", "", "", "", "", "", "", ""];
            isGameActive = true;
            currentPlayer = "X";
            statusDisplay.innerHTML = `Giliran Player: <b style="color:#ff4757;">X</b>`;
            cells.forEach(cell => {
                cell.innerText = "";
                cell.classList.remove("x", "o");
            });
        }
    </script>
</body>
</html>

