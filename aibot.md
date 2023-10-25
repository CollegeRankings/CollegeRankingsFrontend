---
permalink: /aibot
title: AI Bot
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot</title>
    <style>
        .chatbot-container {
            max-width: 100%;
            width: 500px;
            margin: 50px auto;
            background-color: #fff;
            border: 1px solid #e1e1e1;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }
        #header {
            background-color: dodgerblue;
            color: #ffffff;
            padding: 15px;
            border-radius: 10px 10px 0 0;
            text-align: center;
            font-size: 1.5em;
        }
        #conversation {
            height: 400px;
            overflow-y: auto;
            padding: 20px;
            border-bottom: 1px solid #e1e1e1;
        }
        .chatbot-message {
            margin-bottom: 20px;
            animation: fadeIn 0.3s linear;
        }
        .chatbot-text {
            background-color: #f1f1f1;
            color: #222;
            padding: 10px 15px;
            border-radius: 20px;
            display: inline-block;
            max-width: 80%;
        }
        #input-form {
            display: flex;
            align-items: center;
            padding: 10px;
        }
        #input-field {
            flex: 1;
            padding: 10px;
            border-radius: 20px;
            border: 1px solid #e1e1e1;
            outline: none;
        }
        #submit-button {
            background-color: dodgerblue;
            color: #ffffff;
            border: none;
            padding: 10px 20px;
            margin-left: 10px;
            border-radius: 20px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        #submit-button:hover {
            background-color: #45a049;
        }
        @keyframes fadeIn {
            from {opacity: 0;}
            to {opacity: 1;}
        }

    </style>
</head>
<body>
    <div class="chatbot-container">
        <div id="header">Chatbot</div>
        <div id="conversation">
            <!-- Chat messages will appear here -->
        </div>
        <form id="input-form">
            <input id="input-field" type="text" placeholder="Type your message here">
            <button id="submit-button" type="submit">Send</button>
        </form>
    </div>
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const conversation = document.getElementById("conversation");
            const inputField = document.getElementById("input-field");
            const submitButton = document.getElementById("submit-button");
            submitButton.addEventListener("click", function (e) {
                e.preventDefault();
                const userQuestion = inputField.value.trim();
                if (!userQuestion) return; // Don't send empty questions
                const accessCode = prompt("Please enter your access code:");
                if (!accessCode) return; // Don't proceed without access code
                // Send the user's question to the API
                console.log(encodeURIComponent(userQuestion))
                console.log(accessCode)
                fetch(`https://collegerankings.stu.nighthawkcodingsociety.com/api/college/openai?question=${encodeURIComponent(userQuestion)}&code=${accessCode}`, {method: 'GET', mode: 'cors', }).then((response) => response.json()).then((data) => {
                        // Display the answer in the conversation div
                        const chatbotMessage = document.createElement("div");
                        chatbotMessage.classList.add("chatbot-message");
                        const chatbotText = document.createElement("div");
                        chatbotText.classList.add("chatbot-text");
                        chatbotText.textContent = data.answer;
                        chatbotMessage.appendChild(chatbotText);
                        conversation.appendChild(chatbotMessage);
                        // Clear the input field
                        inputField.value = "";
                        inputField.focus();
                    })
                    .catch((error) => {
                        console.error("Error fetching data from the API:", error);
                    });
            });
        });
    </script>
</body>
</html>
