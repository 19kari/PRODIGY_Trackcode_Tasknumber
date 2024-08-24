#html code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" href="styles3.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@200&family=Roboto+Serif&display=swap" rel="stylesheet">
</head>
<body>
    <div id="title">
        <h1>Tic Tac Toe</h1>
    </div>
    <div id="board">
        <div class="square" id="square0"></div>
        <div class="square" id="square1"></div>
        <div class="square" id="square2"></div>
        <div class="square" id="square3"></div>
        <div class="square" id="square4"></div>
        <div class="square" id="square5"></div>
        <div class="square" id="square6"></div>
        <div class="square" id="square7"></div>
        <div class="square" id="square8"></div>
    </div>  
    <div id="endGame">
        <input type="button" value="Restart" id="restartButton" onclick="restartButton()"/>
    </div>
    <script src="js3.js"></script>
</body>
</html>
#CSS code
body {  
    font-family: 'Poppins', sans-serif;
    color: #000000;
}

h1 {
    text-align: center;
}

#board {
    margin-left: auto;
    margin-right: auto;
    width: 375px;
    height: 375px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 5px;
}

.square {
    width: 120px;
    height: 120px;
    border: 1px solid #D3D3D3;
    background-color: #F5F5F5;
    font-size: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.square:hover {
    background-color: #FFFFE0;
}

#restartButton {
    display: block;
    margin-left: auto;
    margin-right: auto;
    height: 40px;
    width: 150px;
    background-color: #FFFFFF;
    border: 1px solid #000000;
    border-radius: 40px;
    font-size: 18px;
}

#restartButton:hover {
    background-color: #000000;
    color: #FFFFFF;
}
#JS code
const board = document.getElementById('board')
const squares = document.getElementsByClassName('square')
const players = ['X', 'O']
let currentPlayer = players[0]
const endMessage = document.createElement('h2')
endMessage.textContent = `X's turn!`
endMessage.style.marginTop = '30px'
endMessage.style.textAlign='center'
board.after(endMessage)

const winning_combinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
]

for(let i = 0; i < squares.length; i++){
    squares[i].addEventListener('click', () => {
        if(squares[i].textContent !== ''){
            return
        }
        squares[i].textContent = currentPlayer
        if(checkWin(currentPlayer)) {
            endMessage.textContent=`Game over! ${currentPlayer} wins!`
            return
        }
        if(checkTie()) {
            endMessage.textContent= `Game is tied!`
            return
        }
        currentPlayer = (currentPlayer === players[0]) ? players[1] : players[0] 
        if(currentPlayer == players[0]) {
            endMessage.textContent= `X's turn!`
        } else {
            endMessage.textContent= `O's turn!`
        }     
    })   
}

function checkWin(currentPlayer) {
    for(let i = 0; i < winning_combinations.length; i++){
        const [a, b, c] = winning_combinations[i]
        if(squares[a].textContent === currentPlayer && squares[b].textContent === currentPlayer && squares[c].textContent === currentPlayer){
            return true
        }
    }
    return false
}

function checkTie(){
    for(let i = 0; i < squares.length; i++) {
        if(squares[i].textContent === '') {
            return false;
        }
    }
    return true
}

function restartButton() {
    for(let i = 0; i < squares.length; i++) {
        squares[i].textContent = ""
    }
    endMessage.textContent=`X's turn!`
    currentPlayer = players[0]
}
