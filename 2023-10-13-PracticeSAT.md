
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA & SAT Form</title>
    <style>
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
            transition: text-shadow 0.3s;
        }
        label[for="gpa"]:hover, label[for="sat"]:hover {
            text-shadow: 5px 5px 8px rgba(0, 0, 0, 0.4); 
        }
        input[type="number"] {
            padding: 10px;
            margin: 5px 0;
            border: 2px solid #ccc;
            border-radius: 5px;
            transition: border 0.3s, transform 0.3s; 
            box-shadow: 3px 3px 6px rgba(0, 0, 0, 0.1); 
        }
        input[type="number"]:focus {
            border: 2px solid dodgerblue;
            transform: scale(1.05); 
        }
        #message {
            margin-top: 10px;
            font-weight: bold;
            display: none;
            animation: fadeIn 2s ease-in-out; 
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
            const gpa = document.getElementById('gpa').value;
            const sat = document.getElementById('sat').value;
            const message = document.getElementById('message');
            const question = document.getElementById('question');
            if (gpa && sat) {
                message.style.display = 'block';
                const questions = [
                    'What\'s your preferred major?',
                    'Do you have a specific location in mind?',
                    'Are you interested in extracurricular activities?',
                    'Tell us about your career goals.'
                    'Favorite extracurricular activity?'
                    'What club do you partake in?'
                    'How do approach hard tests?'
                    'Name your favorite all time subject.'
                ];
                const randomQuestion = questions[Math.floor(Math.random() * questions.length)];
                question.textContent = randomQuestion;
            }
        }
    </script>
</body>
</html>
