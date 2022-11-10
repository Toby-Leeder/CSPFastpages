---
toc: false
layout: post
categories: [project]
title: Chess
---
<a href="https://www.chess.com/learn-how-to-play-chess">
    <button>How do I play chess?</i><button>
<a href="{{ site.baseurl }}/2022/10/23/Feedback.html">
    <button>Report an Issue<button>
<html>
    <head>
        <title></title>
        <meta charset="UTF-8">
        <style>
            .chess-board { border-spacing: 0; border-collapse: collapse; margin-left: 0%; margin-right: 5%;}
            .chess-board th { padding: 2em; }
            .chess-board td { border: 1px solid; width: 1em; height: 1em; text-align: center;}
            .chess-board .light { background: #FFFFFF; }
            .chess-board .dark { background: #808080; }
            .chess-board .selected { background: #f0ff00; }
        </style>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    </head>
    <body>
        <table class="chess-board" id="chess-board">
            <tbody>
                <tr>
                    <th></th>
                    <th>a</th>
                    <th>b</th>
                    <th>c</th>
                    <th>d</th>
                    <th>e</th>
                    <th>f</th>
                    <th>g</th>
                    <th>h</th>
                </tr>
                <tr>
                    <th>8</th>
                    <td  id="a8"></td>
                    <td id="b8"></td>
                    <td  id="c8"></td>
                    <td id="d8"></td>
                    <td  id="e8"></td>
                    <td id="f8"></td>
                    <td  id="g8"></td>
                    <td id="h8"></td>
                </tr>
                <tr>
                    <th>7</th>
                    <td id="a7"></td>
                    <td  id="b7"></td>
                    <td id="c7"></td>
                    <td  id="d7"></td>
                    <td id="e7"></td>
                    <td  id="f7"></td>
                    <td id="g7"></td>
                    <td  id="h7"></td>
                </tr>
                <tr>
                    <th>6</th>
                    <td  id="a6"></td>
                    <td id="b6"></td>
                    <td  id="c6"></td>
                    <td id="d6"></td>
                    <td  id="e6"></td>
                    <td id="f6"></td>
                    <td  id="g6"></td>
                    <td id="h6"></td>
                </tr>
                <tr>
                    <th>5</th>
                    <td id="a5"></td>
                    <td  id="b5"></td>
                    <td id="c5"></td>
                    <td  id="d5"></td>
                    <td id="e5"></td>
                    <td  id="f5"></td>
                    <td id="g5"></td>
                    <td  id="h5"></td>
                </tr>
                <tr>
                    <th>4</th>
                    <td  id="a4"></td>
                    <td id="b4"></td>
                    <td  id="c4"></td>
                    <td id="d4"></td>
                    <td  id="e4"></td>
                    <td id="f4"></td>
                    <td  id="g4"></td>
                    <td id="h4"></td>
                </tr>
                <tr>
                    <th>3</th>
                    <td id="a3"></td>
                    <td  id="b3"></td>
                    <td id="c3"></td>
                    <td  id="d3"></td>
                    <td id="e3"></td>
                    <td  id="f3"></td>
                    <td id="g3"></td>
                    <td  id="h3"></td>
                </tr>
                <tr>
                    <th>2</th>
                    <td  id="a2"></td>
                    <td  id="b2"></td>
                    <td  id="c2"></td>
                    <td  id="d2"></td>
                    <td  id="e2"></td>
                    <td  id="f2"></td>
                    <td  id="g2"></td>
                    <td  id="h2"></td>
                </tr>
                <tr>
                    <th>1</th>
                    <td id="a1"></td>
                    <td  id="b1"></td>
                    <td id="c1"></td>
                    <td  id="d1"></td>
                    <td id="e1"></td>
                    <td  id="f1"></td>
                    <td id="g1"></td>
                    <td  id="h1"></td>
                </tr>
            </tbody>
        </table>
    </body>
    <script>
        //all of the classes to be later extended used
        class piece{
            constructor(_position, _color){
                this.position = _position;
                this.color = _color
            }
            move(move, currentM){
                let currentBoard = chessBoard[currentM];
                if(this.getAvailableMoves().includes(move)) {
                    this.position = move;
                    chessBoard[move] = currentBoard;
                    chessBoard[currentM] = ["OO", undefined];
                }
            }
            getAvailableMoves(){
                let freeMoves = this.getFreeMoves()
                let captures = this.getAvailableCaptures()
                captures.forEach((c) => {
                    freeMoves.push(c);
                })
                return freeMoves;
            }
        }
        class rook extends piece{
            constructor(_position, _color){
                // super is the position constructor, uh basically does some super cool inheritence stuff or something. 
                super(_position, _color);
                // automatically sets the spot on the board which is passed in to this rook
                this.id = "R"
                }   
            //method to return all of the available moves that the piece can make. 
            getTotalMoves(){
                let currentPosition = this.position.split("");
                let moves = [];
                for (var i = 1; i <= 8; i++){
                    var newMove = currentPosition[0] + i;
                    moves[i - 1] = newMove;
                }
                for (var i = 1; i <= 8; i++){
                    var newMove = lettersOnBoard[i - 1] + currentPosition[1];
                    moves.push(newMove);
                }
                let totalMoves = [];
                moves.forEach((c) => {
                    if (c != this.position){
                        totalMoves.push(c);
                    }
                });
                return totalMoves;
            }
            //method to return all of the obstructed moves based on the total moves
            getObstructedMoves(){
                let totalMoves = this.getTotalMoves();
                let obstructedMoves = [];
                let blockedMoves = [];
                let index = -1
                totalMoves.forEach((c) => {
                    if (!obstructedMoves.includes(c)){
                        if (chessBoard[c][0] != "OO"){
                            obstructedMoves.push(c);
                            index++
                            totalMoves.forEach((c) => {
                                try{
                                    if (obstructedMoves[index][1] > this.position[1] && c[1] > obstructedMoves[index][1]){
                                        blockedMoves.push(c)
                                    }
                                    else if (obstructedMoves[index][1] < this.position[1] && c[1] < obstructedMoves[index][1]){
                                        blockedMoves.push(c)
                                    }
                                } catch{}
                                try{
                                    if (lettersOnBoard.indexOf(obstructedMoves[index][0]) > lettersOnBoard.indexOf(this.position[0]) && lettersOnBoard.indexOf(c[0]) > lettersOnBoard.indexOf(obstructedMoves[index][0])){
                                        blockedMoves.push(c)
                                    }
                                    if (lettersOnBoard.indexOf(obstructedMoves[index][0]) < lettersOnBoard.indexOf(this.position[0]) && lettersOnBoard.indexOf(c[0]) < lettersOnBoard.indexOf(obstructedMoves[index][0])){
                                        blockedMoves.push(c)
                                    }
                                } catch{}
                            })
                        } 
                    }
                })
                blockedMoves.forEach((c) => {obstructedMoves.push(c);})
                return obstructedMoves;
            }
            //method to return all of the moves which are not obstructed
            getFreeMoves(){
                let totalMoves = this.getTotalMoves();
                let obstructedMoves = this.getObstructedMoves();
                totalMoves = totalMoves.filter( (c) => !obstructedMoves.includes(c) );
                return totalMoves;
            }
            //method to return the pieces which can be captured. 
            getAvailableCaptures(){
                // defines new variables as other methods in this class which may be useful.
                let totalMoves = this.getTotalMoves();
                let obstructedMoves = this.getObstructedMoves();
                // defines arrays
                let sameRow = [];
                let sameColumn = [];
                let columnNums = [];
                let columnDifs = [];
                let negDifsColumn = [];
                let posDifsColumn = [];
                let rowLets = [];
                let rowNums = [];
                let rowDifs = [];
                let posDifsRow = [];
                let negDifsRow = [];
                let captures = [];
                let finalCaptures = [];
                // finds all of the moves which are in the same row or in the same column as the rook.
                obstructedMoves.forEach((c) => {
                    if (this.position.split("")[0] == c.split("")[0]){
                        sameColumn.push(c);
                    }
                    else if (this.position.split("")[1] == c.split("")[1]){
                        sameRow.push(c);
                    }
                })
                //adds to a new array all of the numbers in the obstructed columns. Also converts it to an Integer
                sameColumn.forEach((c) => {
                    columnNums.push(parseInt(c.split("")[1]));
                })        
                //elipses is a spread function, basically inputs each value in the array as it's own parameter. 
                //this foreach finds the difference between the pieces in the same column and the rooks current position
                columnNums.forEach((c) => {
                    columnDifs.push(c - parseInt(this.position.split("")[1]))
                });
                //this foreach defines two new
                columnDifs.forEach((c) => {
                    if (c < 0) negDifsColumn.push(Math.abs(c)); else posDifsColumn.push(c);
                })
                // finds the minimum positive number and the minimum negative number and converts them to an integer
                var posMinColumn = parseInt(Math.min(...posDifsColumn));
                var negMinColumn = parseInt(Math.min(...negDifsColumn));
                // works backwards to find the position on the board given the smallest differences 
                sameColumn.forEach((c) => {
                    if (parseInt(c.split("")[1]) == parseInt(this.position.split("")[1]) + posMinColumn || parseInt(c.split("")[1]) == parseInt(this.position.split("")[1]) - negMinColumn){
                        captures.push(c)
                    }
                })
                // basically does all of the same stuff but for the rows using the index of the lettersOnBoard array
                sameRow.forEach((c) => {
                    rowLets.push(c.split("")[0]);
                })
                rowLets.forEach((c) => {
                    rowNums.push(lettersOnBoard.indexOf(c) + 1)
                })
                rowNums.forEach((c) => {
                    rowDifs.push(parseInt(c) - (lettersOnBoard.indexOf(this.position.split("")[0]) + 1))
                })
                rowDifs.forEach((c) => {
                    if (c < 0) negDifsRow.push(Math.abs(c)); else posDifsRow.push(c);
                })
                var posMinRow = parseInt(Math.min(...posDifsRow));
                var negMinRow = parseInt(Math.min(...negDifsRow))
                sameRow.forEach((c) => {
                    if ((lettersOnBoard.indexOf(c.split("")[0]) + 1) == (lettersOnBoard.indexOf(this.position.split("")[0]) + posMinRow + 1) || (lettersOnBoard.indexOf(c.split("")[0]) + 1) == (lettersOnBoard.indexOf(this.position.split("")[0]) - negMinRow + 1)){
                        captures.push(c)
                    }
                })
                //checks if captures are the same color or not
                captures.forEach((c) => {
                    if (chessBoard[c][0].split("")[0] != this.color){
                        finalCaptures.push(c);
                    }
                })
                return finalCaptures
            }
        }
        class pawn extends piece{
            constructor(_position, _color){
                // super is the position constructor, uh basically does some super cool inheritence stuff or something. 
                super(_position, _color);
                // automatically sets the spot on the board which is passed in to this pawn using the parent method
                if (_color == "w"){this.direction = 1}
                else if (_color == "b") {this.direction = -1}
                this.hasMoved = 0;
                this.id = "P";
            }
            move(move, currentM){
                super.move(move, currentM)
                this.hasMoved = 1
            }
            getTotalMoves(){
                let moves = [];
                let currentPosition = this.position.split("");
                if(this.hasMoved == 0){
                    moves.push(currentPosition[0] + (parseInt(currentPosition[1]) + (1 * this.direction)))
                    moves.push(currentPosition[0] + (parseInt(currentPosition[1]) + (2 * this.direction)))
                }
                else{
                    moves.push(currentPosition[0] + (parseInt(currentPosition[1]) + (1 * this.direction)))
                }
                return moves;
            }
            getFreeMoves(){
                let moves = this.getTotalMoves();
                let freeMoves = [];
                if (chessBoard[moves[0]][0] == "OO"){
                    freeMoves.push(moves[0]);
                    try{
                        if (chessBoard[moves[1]][0] == "OO"){freeMoves.push(moves[1]);}
                    }catch{}
                }
                return freeMoves;
            } 
            getAvailableCaptures(){
                let captures = [];
                let currentPosition = this.position.split(""); 
                let possibleLets = [
                    lettersOnBoard[lettersOnBoard.indexOf(currentPosition[0]) - 1],
                    lettersOnBoard[lettersOnBoard.indexOf(currentPosition[0]) + 1]
                ];
                possibleLets = possibleLets.filter(c => c != undefined);
                possibleLets.forEach((c) => {
                    let a = parseInt(currentPosition[1]) + (1 * this.direction)
                    let check = c + a
                    if (chessBoard[check][0][0] != this.color && chessBoard[check][0] != "OO"){
                            captures.push(check);
                    }
                })
                return captures;
            }
        }
        class bishop extends piece{
            constructor(_position, _color){
                // super is the position constructor, uh basically does some super cool inheritence stuff or something. 
                super(_position, _color);
                // automatically sets the spot on the board which is passed in to this rook
                this.id = "B"
                }   
            //method to return all of the available moves that the piece can make. 
            getTotalMoves(){
                let currentPosition = this.position;
                let movesLToR = [];
                let movesRToL = [];
                let furthestLeft = currentPosition;
                let furthestRight = currentPosition;
                let bruh = 0;
                while (furthestLeft[0] != "a" && furthestLeft[1] != 1){
                    furthestLeft = lettersOnBoard[lettersOnBoard.indexOf(furthestLeft[0]) - 1] + (furthestLeft[1] - 1);
                }
                while (furthestRight[0] != "h" && furthestRight[1] != 1){
                    furthestRight = lettersOnBoard[lettersOnBoard.indexOf(furthestRight[0]) + 1] + (furthestRight[1] - 1);
                }
                for (i = 0; i < 8 - lettersOnBoard.indexOf(furthestLeft[0]) - furthestLeft[1] + 1; i++){
                    movesLToR.push(lettersOnBoard[lettersOnBoard.indexOf(furthestLeft[0]) + i] + (parseInt(furthestLeft[1]) + i));
                }
                for (i = 0; i < 2 + lettersOnBoard.indexOf(furthestRight[0]) - furthestRight[1]; i++){
                    movesRToL.push(lettersOnBoard[lettersOnBoard.indexOf(furthestRight[0]) - i] + (parseInt(furthestRight[1]) + i));
                }
                let totalMovesLToR = [];
                let totalMovesRToL = []
                movesLToR.forEach((c) => {
                    if (c != this.position){
                        totalMovesLToR.push(c);
                    }
                });
                movesRToL.forEach((c) => {
                    if (c != this.position){
                        totalMovesRToL.push(c);
                    }
                });
                return [totalMovesLToR, totalMovesRToL];
            }
            //method to return all of the obstructed moves based on the total moves
            getObstructedMoves(){
                let totalMoves = this.getTotalMoves();
                let obstructedMovesLToR = [];
                let obstructedMovesRToL = [];
                let blockedMovesLToR = [];
                let blockedMovesRToL = [];
                let index = -1
                // Finds the moves which are behind an obstructed move and also finds all of the obstructed moves. Only for left to right. Does it by compating whether the letter + number is higher or lower. 
                totalMoves[0].forEach((c) => {
                    if (!blockedMovesLToR.includes(c)){
                        if (chessBoard[c][0] != "OO"){
                            obstructedMovesLToR.push(c);
                            index++
                            totalMoves[0].forEach((c) => {
                                try{
                                    if (parseInt(obstructedMovesLToR[index][1]) + lettersOnBoard.indexOf(obstructedMovesLToR[index][0]) > parseInt(this.position[1]) + lettersOnBoard.indexOf(obstructedMovesLToR[index][0]) && parseInt(c[1]) + lettersOnBoard.indexOf(c[0]) > parseInt(obstructedMovesLToR[index][1]) + lettersOnBoard.indexOf(obstructedMovesLToR[index][0])){
                                        blockedMovesLToR.push(c)
                                    }
                                    else if (obstructedMovesLToR[index][1] + lettersOnBoard.indexOf(obstructedMovesLToR[index][0]) < this.position[1] + lettersOnBoard.indexOf(obstructedMovesLToR[index][0]) && c[1] + lettersOnBoard.indexOf(c[0]) < obstructedMovesLToR[index][1] + lettersOnBoard.indexOf(obstructedMovesLToR[index][0])){
                                        blockedMovesLToR.push(c)
                                    }
                                } catch{}
                            })
                        } 
                    }
                })
                index = -1
                // Finds the moves which are behind an obstructed move and also finds all of the obstructed moves. Only for right to left. Does it by finding whether the number is bigger or smaller (realized I was being dumb before but i'm not changing the old code. Because it's only one diaganol though you can easily find if its blocked just by the number.)
                totalMoves[1].forEach((c) => {
                    if (!blockedMovesRToL.includes(c)){
                        if (chessBoard[c][0] != "OO"){
                            obstructedMovesRToL.push(c);
                            index++
                            totalMoves[1].forEach((c) => {
                                try{
                                    if (parseInt(c[1]) > parseInt(obstructedMovesRToL[index][1]) && parseInt(obstructedMovesRToL[index][1]) > parseInt(this.position[1])){
                                        blockedMovesRToL.push(c)
                                    }
                                    else if (parseInt(c[1]) < parseInt(obstructedMovesRToL[index][1]) && parseInt(obstructedMovesRToL[index][1]) < parseInt(this.position[1])){
                                        blockedMovesRToL.push(c)
                                    }
                                } catch{}
                            })
                        } 
                    }
                })
                //seperates the obstructed moves and the blocked moves and returns both. 
                let obstructedMoves = [];
                obstructedMovesLToR.forEach((c) => [obstructedMoves.push(c)])
                obstructedMovesRToL.forEach((c) => [obstructedMoves.push(c)])
                let blockedMoves = [];
                blockedMovesLToR.forEach((c) => {blockedMoves.push(c);})
                blockedMovesRToL.forEach((c) => {blockedMoves.push(c);})
                obstructedMoves = obstructedMoves.filter((c) => !blockedMoves.includes(c))
                return [obstructedMoves, blockedMoves];
            }
            //method to return all of the moves which are not obstructed
            getFreeMoves(){
                let totalMoves = this.getTotalMoves()[0];
                this.getTotalMoves()[1].forEach((c) => {totalMoves.push(c)})
                let obstructedMoves = this.getObstructedMoves()[0];
                this.getObstructedMoves()[1].forEach((c) => {obstructedMoves.push(c)})
                totalMoves = totalMoves.filter((c) => !obstructedMoves.includes(c) );
                return totalMoves;
            }
            //method to return the pieces which can be captured. 
            getAvailableCaptures(){
                let finalCaptures = [];
                let obstructedMoves = this.getObstructedMoves()[0]
                obstructedMoves.forEach((c) => {
                    if (chessBoard[c][0][0] != this.color) {finalCaptures.push(c)}
                })
                console.log(finalCaptures)
                return finalCaptures
            }
        }
    </script>
    <script>
        //useful functions
        function getKeyByValue(object, value, type) {
            if (type == 1){
                return Object.keys(object).find(key => object[key] === value);
            }
            if (type == 2){
                return Object.keys(object).find(key => object[0][key] === value);
            }
            else{
                return "";
            }
        }
        function setBoard(obj){
            chessBoard[obj.position] = [obj.color + obj.id, obj]
        }
        function movePiece(currentM, newM){
            chessBoard[currentM][1].move(newM, currentM)
        }
        let color = false;
        let moving = false;
        function putOnBoard(id) {
            document.getElementById(id).innerHTML = chessPieces[chessBoard[id][0].split("")[0]+chessBoard[id][0].split("")[1]];
            document.getElementById(id).style.fontSize = "100px";
            document.getElementById(id).size = "10px";
            try{document.getElementById(id).classList.remove('selected')}catch{}
            if (id.split("")[1] == "1") color = !color;
            if (color){document.getElementById(id).classList.add('dark');}
            else document.getElementById(id).classList.add('light');
            color = !color;
        }
        function putBoard(){
            for (x in chessBoard){
                putOnBoard(x);
            }
        }
    </script>
    <script>
        // all of the setup
        lettersOnBoard = "abcdefgh";
        chessBoard = {};
        //assigns the board
        for (j = 0; j <= 7; j++){
            letter = lettersOnBoard[j];
            for (i = 1; i <= 8; i++){
                var newKey = letter + i;
                chessBoard[newKey] = ["OO", undefined]
            }
        }
        let currentM = [];
        // assigns chess piece codes to their emoji 
        let chessPieces = {
            wP: "♙",
            wR: "♖",
            wN: "♘",
            wB: "♗",
            wQ: "♕",
            wK: "♔",
            OO: "",
            bP: "♟",
            bR: "♜",
            bN: "♞",
            bB: "♝",
            bQ: "♛",
            bK: "♚",
        }
        //Bishops
        let bishopb1 = new bishop("c8", "b");
        setBoard(bishopb1)
        let bishopb2 = new bishop("f8", "b");
        setBoard(bishopb2)
        let bishopw1 = new bishop("c1", "w");
        setBoard(bishopw1)
        let bishopw2 = new bishop("f1", "w");
        setBoard(bishopw2)
        //Rooks
        let rookb1 = new rook("a8", "b");
        setBoard(rookb1)
        let rookb2 = new rook("h8", "b");
        setBoard(rookb2)
        let rookw1 = new rook("a1", "w");
        setBoard(rookw1)
        let rookw2 = new rook("h1", "w");
        setBoard(rookw2)
        //Pawns
        let pawnw1 = new pawn("a2", "w")
        setBoard(pawnw1)
        let pawnw2 = new pawn("b2", "w")
        setBoard(pawnw2)
        let pawnw3 = new pawn("c2", "w")
        setBoard(pawnw3)
        let pawnw4 = new pawn("d2", "w")
        setBoard(pawnw4)
        let pawnw5 = new pawn("e2", "w")
        setBoard(pawnw5)
        let pawnw6 = new pawn("f2", "w")
        setBoard(pawnw6)
        let pawnw7 = new pawn("g2", "w")
        setBoard(pawnw7)
        let pawnw8 = new pawn("h2", "w")
        setBoard(pawnw8)
        let pawnb1 = new pawn("a7", "b")
        setBoard(pawnb1)
        let pawnb2 = new pawn("b7", "b")
        setBoard(pawnb2)
        let pawnb3 = new pawn("c7", "b")
        setBoard(pawnb3)
        let pawnb4 = new pawn("d7", "b")
        setBoard(pawnb4)
        let pawnb5 = new pawn("e7", "b")
        setBoard(pawnb5)
        let pawnb6 = new pawn("f7", "b")
        setBoard(pawnb6)
        let pawnb7 = new pawn("g7", "b")
        setBoard(pawnb7)
        let pawnb8 = new pawn("h7", "b")
        setBoard(pawnb8)
        //puts the pieces on the board
        putBoard()
        //function to add the board to the table
        //adds the onclick events to each td in the table
        var table = document.getElementById("chess-board");
        if (table != null) {
            for (var i = 0; i < table.rows.length; i++) {
                for (var j = 0; j < table.rows[i].cells.length; j++)
                table.rows[i].cells[j].onclick = function () {
                    move(this);
                };
            }
        }
        function move(id){
            var td = $(id).closest('td').attr('id')
            if (!moving && document.getElementById(td).innerHTML != ""){
                moving = true
                if (td.innerHTML != ""){
                    currentM.push(td);
                    var moves = chessBoard[td][1].getAvailableMoves();
                    moves.forEach((c) => {
                        document.getElementById(c).classList.replace('dark', 'selected');
                        document.getElementById(c).classList.replace('light', 'selected');
                    })
                } 
            }else if (document.getElementById(td).className == "selected"){
                movePiece(currentM[0], td)
                putBoard();
                currentM = [];
                moving = false;
            }else{
                putBoard();
                currentM = [];
                moving = false;
            }
        }
    </script>
    <script>
    </script>
</html>