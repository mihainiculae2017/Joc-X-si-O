<!DOCTYPE html>
<html lang="ro">
<head>
    <meta charset="UTF-8">
    <title>Joc X și O</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            height: 100vh;
            justify-content: center;
            align-items: center;
            background-color: #f0f0f0;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
        }
        .cell {
            position: relative;
        }
        .cell input {
            width: 100%;
            height: 100%;
            opacity: 0;
            position: absolute;
            cursor: pointer;
        }
        .cell label {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            height: 100%;
            background-color: #fff;
            border: 2px solid #000;
            font-size: 2em;
            transition: background-color 0.3s;
        }
        .cell input:checked + label::after {
            content: attr(data-player);
            color: #000;
        }
    </style>
</head>
<body>
    <div class="grid">
        <div class="cell">
            <input type="checkbox" id="cell0" data-index="0">
            <label for="cell0" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell1" data-index="1">
            <label for="cell1" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell2" data-index="2">
            <label for="cell2" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell3" data-index="3">
            <label for="cell3" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell4" data-index="4">
            <label for="cell4" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell5" data-index="5">
            <label for="cell5" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell6" data-index="6">
            <label for="cell6" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell7" data-index="7">
            <label for="cell7" data-player=""></label>
        </div>
        <div class="cell">
            <input type="checkbox" id="cell8" data-index="8">
            <label for="cell8" data-player=""></label>
        </div>
    </div>

    <script>
        const cells = document.querySelectorAll('.cell input');
        let currentPlayer = 'X';
        const gameState = Array(9).fill(null);
        const winningCombinations = [
            [0,1,2],
            [3,4,5],
            [6,7,8],
            [0,3,6],
            [1,4,7],
            [2,5,8],
            [0,4,8],
            [2,4,6]
        ];

        cells.forEach(cell => {
            cell.addEventListener('change', () => {
                const index = cell.getAttribute('data-index');
                if (!gameState[index]) {
                    gameState[index] = currentPlayer;
                    cell.nextElementSibling.setAttribute('data-player', currentPlayer);
                    if (checkWin()) {
                        setTimeout(() => alert(`Jucătorul ${currentPlayer} a câștigat!`), 100);
                        resetGame();
                    } else if (gameState.every(cell => cell)) {
                        setTimeout(() => alert(`Egalitate!`), 100);
                        resetGame();
                    }
                    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                } else {
                    cell.checked = false; // Previne schimbarea unei celule deja ocupate
                }
            });
        });

        function checkWin() {
            return winningCombinations.some(combination => {
                return combination.every(index => gameState[index] === currentPlayer);
            });
        }

        function resetGame() {
            gameState.fill(null);
            cells.forEach(cell => {
                cell.checked = false;
                cell.nextElementSibling.setAttribute('data-player', '');
            });
            currentPlayer = 'X';
        }
    </script>
</body>
</html>
