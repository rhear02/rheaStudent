---
layout: post
title: Voting Chatroom
permalink: /chatroom
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat Platform</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #1c1e24;
            color: #fff;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            width: 80%;
            max-width: 800px;
        }

        h1 {
            font-size: 2em;
            margin-bottom: 10px;
        }

        .card {
            background-color: #2e3a4d;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .card h2 {
            font-size: 1.5em;
            margin-bottom: 10px;
        }

        .card label {
            display: block;
            margin-top: 10px;
        }

        .card select,
        .card input[type="text"],
        .card textarea {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border-radius: 5px;
            border: none;
            background-color: #1c1e24;
            color: #fff;
        }

        .button {
            background-color: #4a90e2;
            color: #fff;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Add a Post</h1>

        <!-- Group and Channel Selection -->
        <div class="card">
            <h2>Select Group and Channel</h2>
            <label for="group">Group:</label>
            <select id="group">
                <option value="general">General</option>
                <option value="private">Private</option>
                <!-- Add more group options here -->
            </select>

            <label for="channel">Channel:</label>
            <select id="channel">
                <option value="announcements">Announcements</option>
                <option value="discussion">Discussion</option>
                <!-- Add more channel options here -->
            </select>

            <button class="button">Select</button>
        </div>

        <!-- Post Creation -->
        <div class="card">
            <h2>Add New Post</h2>
            <label for="title">Title:</label>
            <input type="text" id="title" placeholder="Enter title...">

            <label for="comment">Comment:</label>
            <textarea id="comment" rows="4" placeholder="Enter your comment..."></textarea>

            <button class="button">Add Post</button>
        </div>

        <!-- Post Feed (Example of what a post might look like) -->
        <div class="card">
            <h2>Count 2</h2>
            <p><strong>Added Group and Channel Select</strong></p>
            <p>Channel: Announcements</p>
            <p>User: Thomas Edison</p>
            <p>The page picks Section, here we can select Group and Channel to allow blog filtering.</p>

            <p><strong>JSON content saving through "content" field in database</strong></p>
            <p>Channel: Announcements</p>
            <p>User: Thomas Edison</p>
        </div>
    </div>
</body>
</html>

