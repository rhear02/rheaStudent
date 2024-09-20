---
layout: page
title: snake
description: snake game
permalink: /snake/

---

{% include nav/home.html %}

<style>
    body{
    }
    .wrap{
        margin-left: auto;
        margin-right: auto;

    }

    canvas{
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #BF40BF;
    }
    canvas:focus{
        outline: none;
    }


    /* All screens style */
    #gameover p, #setting p, #menu p{
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a{
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover{
        cursor: pointer;
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before{
        content: ">";
        margin-right: 10px;
    }

    #menu{
        display: block;
    }

    #gameover{
        display: none;
    }

    #setting{
        display: none;
    }

    #setting input{
        display:none;
    }

    #setting label{
        cursor: pointer;
    }

    #setting input:checked + label{
        background-color: #FFF;
        color: #BF40BF;
    }
</style>

<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Snake score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: #CBC3E3; color: #BF40BF">space</span> to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color: #CBC3E3; color: #BF40BF">space</span> to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <!-- Settings Screen -->
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color: #CBC3E3; color: #BF40BF">space</span> to go back to playing</p>
            <a id="new_game2" class="link-alert">new game</a>
            <br>
            <p>Speed:
                <input id="speed1" type="radio" name="speed" value="120" checked/>
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75"/>
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">Fast</label>
            </p>
            <p>Wall:
                <input id="wallon" type="radio" name="wall" value="1" checked/>
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0"/>
                <label for="walloff">Off</label>
            </p>
        </div>
    </div>
</div>

<script>
    (function(){
        /* Attributes of Game */
        /////////////////////////////////////////////////////////////
        // Canvas & Context
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        // HTML Game IDs
        const SCREEN_SNAKE = 0;
        const screen_snake = document.getElementById("snake");
        const ele_score = document.getElementById("score_value");
        const speed_setting = document.getElementsByName("speed");
        const wall_setting = document.getElementsByName("wall");
        // HTML Screen IDs (div)
        const SCREEN_MENU = -1, SCREEN_GAME_OVER=1, SCREEN_SETTING=2;
        const screen_menu = document.getElementById("menu");
        const screen_game_over = document.getElementById("gameover");
        const screen_setting = document.getElementById("setting");
        // HTML Event IDs (a tags)
        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");
        const button_new_game2 = document.getElementById("new_game2");
        const button_setting_menu = document.getElementById("setting_menu");
        const button_setting_menu1 = document.getElementById("setting_menu1");
        // Game Control
        const BLOCK = 10;   // size of block rendering
        let SCREEN = SCREEN_MENU;
        let snake;
        let snake_dir;
        let snake_next_dir;
        let snake_speed;
        let food = {x: 0, y: 0};
        let score;
        let wall;
        /* Display Control */
        /////////////////////////////////////////////////////////////
        let showScreen = function(screen_opt){
            SCREEN = screen_opt;
            switch(screen_opt){
                case SCREEN_SNAKE:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "none";
                    break;
                case SCREEN_GAME_OVER:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "block";
                    break;
                case SCREEN_SETTING:
                    screen_snake.style.display = "none";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "block";
                    screen_game_over.style.display = "none";
                    break;
            }
        }
        /* Actions and Events  */
        /////////////////////////////////////////////////////////////
        window.onload = function(){
            // HTML Events to Functions
            button_new_game.onclick = function(){newGame();};
            button_new_game1.onclick = function(){newGame();};
            button_new_game2.onclick = function(){newGame();};
            button_setting_menu.onclick = function(){showScreen(SCREEN_SETTING);};
            button_setting_menu1.onclick = function(){showScreen(SCREEN_SETTING);};
            // speed
            setSnakeSpeed(150);
            for(let i = 0; i < speed_setting.length; i++){
                speed_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < speed_setting.length; i++){
                        if(speed_setting[i].checked){
                            setSnakeSpeed(speed_setting[i].value);
                        }
                    }
                });
            }
            // wall setting
            setWall(1);
            for(let i = 0; i < wall_setting.length; i++){
                wall_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < wall_setting.length; i++){
                        if(wall_setting[i].checked){
                            setWall(wall_setting[i].value);
                        }
                    }
                });
            }
            // Prevent default scrolling behavior for arrow keys and spacebar to start game
            window.addEventListener("keydown", function(evt) {
                // Prevent default browser action (scrolling) on arrow key press
                if (evt.code === "ArrowUp" || evt.code === "ArrowDown" || evt.code === "ArrowLeft" || evt.code === "ArrowRight") {
                    evt.preventDefault();
                }
                // Spacebar detected for starting the game
                if (evt.code === "Space" && SCREEN !== SCREEN_SNAKE) {
                    newGame();
                }
            }, true);
        }
        /* Snake is on the Go (Driver Function)  */
        /////////////////////////////////////////////////////////////
        let mainLoop = function(){
            let _x = snake[0].x;
            let _y = snake[0].y;
            snake_dir = snake_next_dir;   // read async event key
            switch(snake_dir){
                case 0: _y--; break;
                case 1: _x++; break;
                case 2: _y++; break;
                case 3: _x--; break;
            }
            snake.pop(); // tail is removed
            snake.unshift({x: _x, y: _y}); // head is new in new position/orientation
            // Wall Checker
            if(wall === 1){
                if (snake[0].x < 0 || snake[0].x === canvas.width / BLOCK || snake[0].y < 0 || snake[0].y === canvas.height / BLOCK){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }else{
                for(let i = 0, x = snake.length; i < x; i++){
                    if(snake[i].x < 0){
                        snake[i].x = canvas.width / BLOCK - 1;
                    }
                    if(snake[i].x === canvas.width / BLOCK){
                        snake[i].x = 0;
                    }
                    if(snake[i].y < 0){
                        snake[i].y = canvas.height / BLOCK - 1;
                    }
                    if(snake[i].y === canvas.height / BLOCK){
                        snake[i].y = 0;
                    }
                }
            }
            // Collision Check
            for(let i = 1, x = snake.length; i < x; i++){
                if(snake[0].x === snake[i].x && snake[0].y === snake[i].y){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }
            // Food Detector
            if(snake[0].x === food.x && snake[0].y === food.y){
                score += 1;
                ele_score.innerHTML = score;
                snake[snake.length] = {x: snake[0].x, y: snake[0].y};
                // Set New Food
                setFood();
            }
            // Make background
            ctx.fillStyle = "#CBC3E3";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            // Draw Snake
            for(let i = 0, x = snake.length; i < x; i++){
                ctx.fillStyle = "#BF40BF";
                ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
            }
            // Draw Food
            ctx.fillStyle = "#BF40BF";
            ctx.fillRect(food.x * BLOCK, food.y * BLOCK, BLOCK, BLOCK);
            setTimeout(mainLoop, snake_speed);
        }
        /* Snake Food  */
        
        let setFood = function(){
            food = {
                x: Math.floor(Math.random() * canvas.width / BLOCK),
                y: Math.floor(Math.random() * canvas.height / BLOCK)
            }
        }
        /* Snake Initialization (Driver Helper)  */
        
        let newGame = function(){
            showScreen(SCREEN_SNAKE);
            snake = [{x: 5, y: 5}];   // snake body
            score = 0;
            ele_score.innerHTML = score;
            snake_next_dir = 1;   // begin in moving right
            setFood();   // place the first food
            mainLoop();   // move on
        }
        let setSnakeSpeed = function(val){snake_speed = val;}
        let setWall = function(val){wall = val;}
        /* Key Listener  */
        
        canvas.onkeydown = function(evt){
            evt.preventDefault(); // Prevent default scrolling behavior when controlling the snake
            changeDir(evt.keyCode);
        };
        let changeDir = function(key){
            if(key === 38 && snake_dir !== 2){ // up
                snake_next_dir = 0;
            }else if(key === 39 && snake_dir !== 3){ // right
                snake_next_dir = 1;
            }else if(key === 40 && snake_dir !== 0){ // down
                snake_next_dir = 2;
            }else if(key === 37 && snake_dir !== 1){ // left
                snake_next_dir = 3;
            }
        }
    })();
</script>

<body style="background-color:pink;">
<p style="border:  2px solid purple;"> Click on light purple square to start playing!
