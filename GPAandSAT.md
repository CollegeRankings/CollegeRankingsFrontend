---
permalink: /GPAandSATrecomendation
title: GPA and SAT Recomendation
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA & SAT Form</title>
    <style>
        /* Style for the animated input field */
        .animated-input {
            display: flex;
            flex-direction: column;
            max-width: 300px;
            margin: 0 auto;
        }
        label[for="gpa"], label[for="sat"] {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-weight: bold;
            font-size: 18px;
            text-shadow: 2px 2px 3px rgba(0, 0, 0, 0.2);
            transition: text-shadow 0.3s; /* Added transition property */
        }
        label[for="gpa"]:hover, label[for="sat"]:hover {
            text-shadow: 5px 5px 8px rgba(0, 0, 0, 0.4); /* Shadow effect on hover */
        }
        input[type="number"] {
            padding: 10px;
            margin: 5px 0;
            border: 2px solid #ccc;
            border-radius: 5px;
            transition: border 0.3s, transform 0.3s; /* Added transform property */
            box-shadow: 3px 3px 6px rgba(0, 0, 0, 0.1); /* Adding box shadow */
        }
        input[type="number"]:focus {
            border: 2px solid dodgerblue;
            transform: scale(1.05); /* Scale animation on focus */
        }
        #message {
            margin-top: 10px;
            font-weight: bold;
            display: none;
            animation: fadeIn 2s ease-in-out; /* Adding fade-in animation */
        }
        button {
            display: block;
            margin: 0 auto;
            padding: 10px 20px;
            background-color: dodgerblue;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: deepskyblue;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>
    <div class="animated-input">
        <label for="gpa">GPA:</label>
        <input type="number" id="gpa" placeholder="Enter GPA">
    </div>
    <div class="animated-input">
        <label for="sat">SAT Score:</label>
        <input type="number" id="sat" placeholder="Enter SAT Score">
    </div>
    <button onclick="showFitCollegeMessage()">Submit</button>
    <div id="message">Generating a fit college for you</div>
    <div id="question"></div>
    <script>
        function showFitCollegeMessage() {
            // Get the message element
            var messageElement = document.getElementById('message');
            // Display the message element
            messageElement.style.display = 'block';
        }
    </script>
</body>
</html>
