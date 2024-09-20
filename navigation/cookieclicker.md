---
layout: page
title: cookieclicker
description: cookie game
permalink: /cookieclicker/

---

<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <link href="https://fonts.googleapis.com/css2?family=Cookie&display=swap" rel="stylesheet">
   <style>
       body {
           display: flex;
           flex-direction: column;
           align-items: center;
           justify-content: center;
           background-color: #f1e7d6;
           font-family: Arial, sans-serif;
           height: 100vh;
           margin: 0;
           padding: 0;
       }

       header {
           width: 100%;
           height: 100px; /* Adjust this height to fit your navigation bar */
           position: fixed;
           top: 0;
           left: 0;
           z-index: 1000; /* Ensures the header is on top of other content */
       }

       body {
           padding-top: 120px; /* Ensure content doesn't overlap with the fixed header */
       }

       h1 {
           font-family: 'Cookie', cursive;
           color: #333; /* Change to black text */
           font-size: 3rem;
           margin: 0;
           position: relative;
           top: 50px; /* Lower the position of the title */
           text-align: center;
       }

       #gameContainer {
           position: relative;
           text-align: center;
           margin-top: 100px; /* Adjust margin as needed */
       }

       #cookie {
           width: 150px; /* Adjust the size of the cookie */
           height: 150px;
           cursor: pointer;
           transition: transform 0.1s ease;
       }

       #cookie:active {
           transform: scale(0.9);
       }

       #score {
           margin-top: 20px;
           font-size: 24px;
           color: #333;
       }

       #youWin {
           font-size: 32px;
           color: #E74C3C;
           margin-top: 50px;
           display: none;
       }

       #playAgain {
           background-color: #2ecc71;
           color: white;
           padding: 10px 20px;
           border: none;
           border-radius: 8px;
           font-size: 16px;
           cursor: pointer;
           display: none;
           margin-top: 20px;
       }
   </style>
</head>
<body>

   <header>
       <!-- Navigation bar content here -->
   </header>

   <h1>Cookie Clicker</h1>
   <div id="gameContainer">
       <!-- Set the alt attribute to empty to avoid text displaying behind the image -->
       <img id="cookie" src="https://prettysimplesweet.com/wp-content/uploads/2020/07/Big-Chocolate-Chip-Cookies-150x150.jpg" alt="">
       <div id="score">Cookies: 0</div>

       <div id="youWin">You Win! Cookies are raining down!</div>
       <button id="playAgain" onclick="resetGame()">Play Again</button>
   </div>

   <script>
       let cookies = 0;
       let cookiesPerClick = 1;
       let autoClicker = null;

       const scoreElement = document.getElementById("score");
       const cookieElement = document.getElementById("cookie");
       const youWinElement = document.getElementById("youWin");
       const playAgainButton = document.getElementById("playAgain");

       cookieElement.addEventListener("click", function () {
           cookies += cookiesPerClick;
           updateScore();
           checkWinCondition();
       });

       function updateScore() {
           scoreElement.textContent = `Cookies: ${cookies}`;
       }

       function checkWinCondition() {
           if (cookies >= 10000) {
               clearInterval(autoClicker);
               cookieElement.style.display = "none";
               youWinElement.style.display = "block";
               playAgainButton.style.display = "block";
               // Raining cookies effect
               document.body.style.backgroundImage = 'url("https://prettysimplesweet.com/wp-content/uploads/2020/07/Big-Chocolate-Chip-Cookies-150x150.jpg")';
               document.body.style.backgroundRepeat = "repeat";
           }
       }

       function resetGame() {
           cookies = 0;
           cookiesPerClick = 1;
           updateScore();
           youWinElement.style.display = "none";
           playAgainButton.style.display = "none";
           cookieElement.style.display = "block";
           document.body.style.backgroundImage = "none";
           clearInterval(autoClicker);
           autoClicker = null;
       }
   </script>

</body>
</html>