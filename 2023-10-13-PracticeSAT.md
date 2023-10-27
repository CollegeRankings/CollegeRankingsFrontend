
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA & SAT Form</title>
    <style>
        /* Your CSS styles here */
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
                // Simulate a delay using setTimeout
                setTimeout(function() {
                    const questions = [
                        'What\'s your preferred major?',
                        'Do you have a specific location in mind?',
                        'Are you interested in extracurricular activities?',
                        'Tell us about your career goals.',
                        'Favorite extracurricular activity?',
                        'What club do you partake in?',
                        'How do you approach hard tests?',
                        'Name your favorite all-time subject.'
                    ];
                    const randomQuestion = questions[Math.floor(Math.random() * questions.length)];
                    question.textContent = randomQuestion;
                }, 2000); // Adjust the time (in milliseconds) as needed
            }
        }
    </script>
</body>
</html>

