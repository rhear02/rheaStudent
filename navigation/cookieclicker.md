---
layout: cookieclicker
title: cookieclicker
description: cookies
permalink: /cookieclicker/

---

{% include nav/home.html %}

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 200vh;
            background-color: #F0F0F0;
        }
        #cookie {
            width: 250px; /* Increase the cookie size */
            cursor: pointer;
            margin-bottom: 20px;
        }
        #score {
            font-size: 32px; /* Increase score text size */
            color: white;
        }
        .game-container {
            background-color: #333; /* Add a background color */
            padding: 30px; /* Increase padding for a bigger box */
            border-radius: 10px; /* Rounded corners for a smoother look */
            width: 350px; /* Increase container width */
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>Cookie Clicker</h1>
    <img src="{{ site.baseurl }}/images/cookie.png" alt="Cookie" id="cookie">
    <div id="score">Score: 0</div>
    <audio id="clickSound" src="{{ site.baseurl}}/assets/click.wav"></audio>
    <script>
        let score = 0;
        const cookie = document.getElementById('cookie');
        const scoreDisplay = document.getElementById('score');
        const clickSound = document.getElementById('clickSound');
        cookie.addEventListener('click', function() {
            score++;
            scoreDisplay.textContent = 'Score: ' + score;
            clickSound.play();
        });
    </script>
</body>
</html>

<body style="background-color:pink;">