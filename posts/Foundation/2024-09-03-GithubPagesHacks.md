---
layout: post
title: Github Pages Submenu
courses: {'csp': {'week': 3}}
type: ccc
---
 <html lang="en"> <!--means in html  -->
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Food Submenu</title>
    <style>
        /* Styling for the submenu */
        .submenu {
            display: flex;
            justify-content: center;
            background-color: #f8f9fa;
            padding: 10px;
        }
        .submenu a {
            margin: 0 15px;
            text-decoration: none;
            color: #007bff;
            font-weight: bold;
        }
        .submenu a:hover {
            color: #0056b3;
            text-decoration: underline;
        }
    </style>
</head>

<body>
 <div class="submenu">
        <a href="/rheaStudent/breakfast">Breakfast</a> <!-- links to breakfast page -->
        <a href="/rheaStudent/lunch">Lunch</a>
        <a href="/rheaStudent/dinner">Dinner</a>
        <a href="/rheaStudent/dessert">Dessert</a>
    </div>
     <p>Select an option above to start.</p>
</body>