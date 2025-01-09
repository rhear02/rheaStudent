---
layout: post
title: Genres
description: Genres
permalink: /voteforthegoat/genres/
comments: true
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Music Genre Poll</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin: 0;
            background-color: pink; /* Background stays pink */
            overflow-y: auto; /* Allows scrolling */
        }
        .container {
            text-align: center;
            padding: 20px;
            background-color: transparent;
        }
        .vinyl-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            margin-bottom: 20px;
        }
        .vinyl-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            background: transparent; /* Ensures transparency */
        }
        .vinyl-item button {
            background: transparent; /* Removes button background */
            border: none;
            cursor: pointer;
            outline: none;
        }
        .vinyl-item img {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
            transition: transform 0.3s;
            background-color: transparent; /* Ensures no background color */
            box-shadow: none; /* Removes shadow if unwanted */
        }
        .vinyl-item img:hover {
            transform: scale(1.1);
        }
        .vinyl-item span {
            margin-top: 8px;
            font-size: 16px;
            color: #FFF; /* Text color changed to white */
        }
        .comments-section {
            display: none;
            margin-top: 20px;
            width: 80%;
            max-width: 600px;
        }
        .comments-section h3 {
            margin-top: 0;
        }
        .comment-box {
            display: flex;
            margin-bottom: 10px;
        }
        .comment-box textarea {
            flex: 1;
            padding: 10px;
            font-size: 14px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .comment-box button {
            padding: 10px 20px;
            font-size: 14px;
            margin-left: 10px;
            background-color: #6C63FF;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .comment-box button:hover {
            background-color: #554FD6;
        }
        .comments-list {
            list-style-type: none;
            padding: 0;
        }
        .comments-list li {
            padding: 10px;
            background-color: #000;
            color: #FFF;
            border-radius: 5px;
            margin-bottom: 5px;
        }
        .username {
            font-weight: bold;
            color: #FFDD57;
            margin-right: 5px;
        }
        .chatroom-button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            background-color: #FF6347;
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            transition: background-color 0.3s;
        }
        .chatroom-button:hover {
            background-color: #FF4500;
        }
    </style>
</head>
<a href="/flocker_frontend/Chatroom" class="chatroom-button">Go to Chatroom</a>  

<body>
    <div class="container">
        <div class="vinyl-grid">
            <div class="vinyl-item">
                <button onclick="vote('Rock')">
                    <img src="/flocker_frontend/images/vinyl2.png" alt="Rock Vinyl">
                </button>
                <span>Rock</span>
            </div>
            <div class="vinyl-item">
                <button onclick="vote('Pop')">
                    <img src="/flocker_frontend/images/vinyl2.png" alt="Pop Vinyl">
                </button>
                <span>Pop</span>
            </div>
            <div class="vinyl-item">
                <button onclick="vote('Hip-Hop')">
                    <img src="/flocker_frontend/images/vinyl2.png" alt="Hip-Hop Vinyl">
                </button>
                <span>Hip-Hop</span>
            </div>
            <div class="vinyl-item">
                <button onclick="vote('Jazz')">
                    <img src="/flocker_frontend/images/vinyl2.png" alt="Jazz Vinyl">
                </button>
                <span>Jazz</span>
            </div>
            <div class="vinyl-item">
                <button onclick="vote('Classical')">
                    <img src="/flocker_frontend/images/vinyl2.png" alt="Classical Vinyl">
                </button>
                <span>Classical</span>
            </div>
            <div class="vinyl-item">
                <button onclick="vote('Electronic')">
                    <img src="/flocker_frontend/images/vinyl2.png" alt="Electronic Vinyl">
                </button>
                <span>Electronic</span>
            </div>
        </div>
        <label for="genre">Pick Your Favorite Genre Out of These!</label>
        
        <!-- Comments Section -->
        <div class="comments-section" id="comments-section">
            <h3>Comment Your Opinion!</h3>
            <div class="comment-box">
                <textarea id="commentInput" placeholder="Write a comment..."></textarea>
                <button onclick="addComment()">Submit</button>
            </div>
            <ul class="comments-list" id="commentsList"></ul>
        </div>
    </div>

    <script>
        function vote(genre) {
            alert(genre + " selected!");
            // Display the comments section after a genre is selected
            document.getElementById('comments-section').style.display = 'block';
        }

        function getRandomUsername() {
            const adjectives = ["Mysterious", "Cool", "Chill", "Groovy", "Silent"];
            const animals = ["Penguin", "Fox", "Tiger", "Panda", "Eagle"];
            const randomAdjective = adjectives[Math.floor(Math.random() * adjectives.length)];
            const randomAnimal = animals[Math.floor(Math.random() * animals.length)];
            const randomNumber = Math.floor(Math.random() * 1000);
            return `${randomAdjective}${randomAnimal}${randomNumber}`;
        }

        function addComment() {
            const commentInput = document.getElementById('commentInput');
            const commentText = commentInput.value.trim();
            if (commentText !== "") {
                const commentItem = document.createElement('li');
                
                // Create username element
                const usernameSpan = document.createElement('span');
                usernameSpan.classList.add('username');
                usernameSpan.textContent = getRandomUsername() + ": ";
                
                // Append username and comment text
                commentItem.appendChild(usernameSpan);
                commentItem.appendChild(document.createTextNode(commentText));
                
                // Add comment to the comments list
                document.getElementById('commentsList').appendChild(commentItem);
                
                // Clear input field
                commentInput.value = '';
            } else {
                alert("Please enter a comment before submitting.");
            }
        }
    </script>
</body>
</html>
