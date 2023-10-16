---
layout: default
title: College Rankings
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <title>College Rankings</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .hero-section {
            height: 60vh;
            background-image: url('https://i0.wp.com/www.nationalreview.com/wp-content/uploads/2018/08/students-campus-university-of-pennsylvania.jpg?fit=789%2C460&ssl=1');
            background-size: cover;
            background-position: center;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            position: relative; /* Add this line to make the background overlay work */
        }
        /* Background overlay */
        .hero-section::before {
            content: "";
            background: rgba(0, 0, 0, 0.5); /* Adjust the transparency by changing the last value (0.5) */
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            z-index: -1; /* Place it behind the text content */
        }
        .hero-section h1 {
            font-size: 80px;
            margin-bottom: 20px;
            background: rgba(0, 0, 0, 0.7);
        }
        .hero-section p {
            font-size: 40px;
            margin-bottom: 20px;
            background: rgba(0, 0, 0, 0.77);
        }
        .top-colleges, .recommendations {
            padding: 50px 0;
        }
        .college-card {
            margin-bottom: 30px;
        }
    </style>
</head>
<body>

<!-- Hero Section -->
<section class="hero-section">
    <div>
        <h1>Welcome to College Rankings</h1>
        <p>Find the best colleges and get personalized recommendations</p>
    </div>
</section>

<!-- Top Colleges Section -->

<section class="top-colleges container">
    <h2 class="text-center">Top Ranked Colleges</h2>
    <div class="row" id="college-list"></div> <!-- This is where we'll display the college information -->
    <div class="text-center mt-4">
        <a href="#" class="btn btn-primary btn-lg font-weight-bold" id="viewMoreColleges">View More Colleges</a>
    </div>
</section>

<script>
    // Function to get the correct link for "View More Colleges" based on the hostname
    function getCollegesLink() {
        if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
            return "/colleges";
        } else {
            return "https://collegerankings.github.io/CollegeRankingsFrontend/colleges";
        }
    }

    // Update the "View More Colleges" link dynamically
    const viewMoreCollegesLink = document.getElementById('viewMoreColleges');
    viewMoreCollegesLink.href = getCollegesLink();
</script>

<!-- Personalized Recommendations Section -->
<section class="recommendations container">
    <h2 class="text-center">Get Personalized Recommendations</h2>
    <p class="text-center">Answer a few questions and get college recommendations tailored just for you</p>
    <div class="text-center mt-4">
        <a href="#" class="btn btn-primary btn-lg font-weight-bold" id="getStartedButton">Get Started</a>
    </div>
</section>

<script>
    // Function to get the correct link for "Get Started" based on the hostname
    function getGetStartedLink() {
        if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
            return "/GPAandSATrecommendation";
        } else {
            return "https://collegerankings.github.io/CollegeRankingsFrontend/GPAandSATrecommendation";
        }
    }

    // Update the "Get Started" link dynamically
    const getStartedButton = document.getElementById('getStartedButton');
    getStartedButton.href = getGetStartedLink();
</script>


<script>
    // Function to fetch and display college information
    async function fetchColleges() {
        try {
            const response = await fetch('https://collegerankings.stu.nighthawkcodingsociety.com/api/college/colleges'); // Replace with your API URL
            const data = await response.json();

            // Select the div where you want to display the colleges
            const collegeList = document.getElementById('college-list');

            // Loop through the first 3 colleges (assuming API returns an array of colleges)
            data.slice(0, 3).forEach(college => {
                // Create a div to hold college card
                const collegeCard = document.createElement('div');
                collegeCard.classList.add('col-lg-4', 'col-md-6', 'mb-4'); // Adjust the column size here
                collegeCard.innerHTML = `
                    <div class="card">
                        <img src="${college.image || placeholderImageUrl}" class="card-img-top" alt="${college.name}">
                        <div class="card-body">
                            <h5 class="card-title">${college.name}</h5>
                            <p class="card-text">Location: ${college.city}, ${college.state}</p>
                            <p class="card-text">Ranking: ${college.ranking || 'Not Available'}</p>
                            <a href="${getCollegeDetailsLink(college.id)}" class="btn btn-primary view-details-btn">View Details</a>
                        </div>
                    </div>
                `;
                collegeList.appendChild(collegeCard);
            });

        function getCollegeDetailsLink(collegeId) {
            let baseUrl;

            if (location.hostname === "localhost" || location.hostname === "127.0.0.1") {
                baseUrl = "/colleges/";
            } else {
                baseUrl = "https://collegerankings.github.io/CollegeRankingsFrontend/colleges/";
            }

            return `${baseUrl}college_details?id=${collegeId}`;
        }

        } catch (error) {
            console.error('Error fetching data:', error);
        }
    }

    // Call the fetchColleges function when the page loads
    window.addEventListener('load', fetchColleges);
</script>

<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
