---
permalink: /collegerecommendation
title: College Recommendation
---

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>College Recommendations</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">
    <style>
        /* Your Animated Input Field Styles */
        .animated-input {
            display: flex;
            flex-direction: column;
            max-width: 300px;
            margin: 0 auto;
        }
        label[for="gpa"],
        label[for="sat"] {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-weight: bold;
            font-size: 18px;
            text-shadow: 2px 2px 3px rgba(0, 0, 0, 0.2);
            transition: text-shadow 0.3s;
        }
        label[for="gpa"]:hover,
        label[for="sat"]:hover {
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
        /* Your College Styles */
        .college-body {
            background-color: #f4f7f6;
            font-family: 'Arial', sans-serif;
        }
        .college-container {
            margin-top: 50px;
        }
        .college-h1 {
            color: #333;
            text-align: center;
            margin-bottom: 40px;
        }
        .college-search-bar {
            margin-bottom: 30px;
            border-radius: 30px;
            padding: 20px;
            font-size: 18px;
        }
        .college-card {
            transition: transform 0.3s ease-in-out;
            border-radius: 20px;
            overflow: hidden;
            border: none;
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.1);
        }
        .college-card:hover {
            transform: scale(1.05);
        }
        .college-card-img-top {
            height: 200px;
            object-fit: cover;
        }
        .college-card-title,
        .college-card-text {
            color: #333;
        }
        .college-btn-primary {
            background-color: #3498db;
            border: none;
            border-radius: 20px;
            padding: 10px 20px;
            font-size: 16px;
        }
        .college-btn-primary:hover {
            background-color: #48a2ca;
        }
        @media (max-width: 768px) {
            .college-h1 {
                font-size: 24px;
            }
        }
    </style>

</head>

<body class="college-body">
    <div class="container college-container">
        <div class="animated-input">
            <label for="gpa">GPA</label>
            <input type="number" class="form-control college-search-bar" id="gpa" placeholder="Enter your GPA">
            <label for="sat">SAT Score</label>
            <input type="number" class="form-control college-search-bar" id="sat" placeholder="Enter your SAT score">
            <button id="submit" class="college-btn-primary">Find Colleges</button>
        </div>
        <br>
        <br>
        <div id="colleges" class="row"></div>
    </div>
    <script>
        document.getElementById('submit').addEventListener('click', function () {
            const gpa = document.getElementById('gpa').value;
            const sat = document.getElementById('sat').value;
            const collegesContainer = document.getElementById('colleges');
            collegesContainer.innerHTML = '';
            console.log(`https://collegerankings.stu.nighthawkcodingsociety.com/api/college/mlrecommendation?gpa=${gpa}&sat=${sat}`);
            fetch(`https://collegerankings.stu.nighthawkcodingsociety.com/api/college/mlrecommendation?gpa=${gpa}&sat=${sat}`)
                .then(response => response.json())
                .then(data => {
                    data.forEach(college => {
                        const placeholderImageUrl = "https://www.avantistones.com/images/noImage.png"; // Add your placeholder image URL here
                        const collegeCard = document.createElement('div');
                        collegeCard.className = "col-md-4";
                        collegeCard.innerHTML = `
                            <div class="card college-card mb-3">
                                <img src="${college.image || placeholderImageUrl}" class="card-img-top college-card-img-top" alt="${college.name}">
                                <div class="card-body">
                                    <h5 class="card-title college-card-title">${college.name}</h5>
                                    <p class="card-text college-card-text">${college.city}, ${college.state}</p>
                                    <p class="card-text college-card-text">Ranking: ${college.ranking || 'Not Available'}</p>
                                    <button data-college-id="${college.id}" class="btn btn-primary view-details-btn">View Details</button>
                                </div>
                            </div>
                        `;
                        collegesContainer.appendChild(collegeCard);
                        const detailsButtons = document.querySelectorAll('.view-details-btn');
                        detailsButtons.forEach(btn => {
                            btn.addEventListener('click', (e) => {
                                const collegeId = e.target.getAttribute('data-college-id');
                                let baseUrl;
                                if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
                                    baseUrl = "/colleges/";
                                } else {
                                    baseUrl = "https://collegerankings.github.io/CollegeRankingsFrontend/colleges/";
                                }
                                console.log('${baseUrl}college_details?id=${collegeId}')
                                location.href = `${baseUrl}college_details?id=${collegeId}`;
                            });
                        });
                    });
                })
                .catch(error => {
                    console.error('Error:', error);
                });
        });
    </script>

</body>

</html>
