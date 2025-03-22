# INTERACTIVE-CROSSWORD
VOCABULARY CROSSWORD
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Crossword</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .grid { display: grid; grid-template-columns: repeat(25, 30px); justify-content: center; }
        .cell { width: 30px; height: 30px; border: 1px solid black; text-align: center; font-size: 18px; }
        input { width: 100%; height: 100%; text-align: center; border: none; font-size: 18px; }
    </style>
</head>
<body>
    <h1>Interactive Crossword</h1>
    <div class="grid" id="crossword"></div>
    <button onclick="checkAnswers()">Check Answers</button>
    <p id="result"></p>
    
    <script>
        const gridSize = 25;
        const words = [
            { word: "RELEVANCE", row: 0, col: 0, direction: "H" },
            { word: "FULLDISCLOSURE", row: 2, col: 5, direction: "V" },
            { word: "UNBIASED", row: 4, col: 3, direction: "H" },
            { word: "PARTNERSHIP", row: 6, col: 1, direction: "V" },
            { word: "OBJECTIVITY", row: 8, col: 2, direction: "H" },
            { word: "CONSERVATISM", row: 10, col: 4, direction: "V" },
            { word: "BUSINESSENTITY", row: 1, col: 12, direction: "H" },
            { word: "CORPORATION", row: 5, col: 18, direction: "V" },
            { word: "OPTIMISTIC", row: 7, col: 7, direction: "H" },
            { word: "MOSTLIKELYSCENARIO", row: 14, col: 6, direction: "H" },
            { word: "SOLEPROPIETORSHIP", row: 20, col: 0, direction: "H" }
        ];

        function createGrid() {
            const crossword = document.getElementById("crossword");
            for (let i = 0; i < gridSize; i++) {
                for (let j = 0; j < gridSize; j++) {
                    const cell = document.createElement("div");
                    cell.classList.add("cell");
                    const input = document.createElement("input");
                    input.setAttribute("maxlength", "1");
                    cell.appendChild(input);
                    crossword.appendChild(cell);
                }
            }
        }
        
        function checkAnswers() {
            const inputs = document.querySelectorAll(".cell input");
            let correct = true;
            words.forEach(({ word, row, col, direction }) => {
                for (let i = 0; i < word.length; i++) {
                    let index = direction === "H" ? row * gridSize + (col + i) : (row + i) * gridSize + col;
                    if (inputs[index].value.toUpperCase() !== word[i]) {
                        correct = false;
                    }
                }
            });
            document.getElementById("result").innerText = correct ? "Correct! Well done!" : "Some answers are incorrect, try again!";
        }

        createGrid();
    </script>
</body>
</html>

