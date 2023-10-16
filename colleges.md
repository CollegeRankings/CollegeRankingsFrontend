---
permalink: /colleges
title: Colleges
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Colleges</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">
    <style>
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

        .college-card-title, .college-card-text {
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
    <h1 class="college-h1">Explore Colleges</h1>
    <input type="text" id="search-bar" class="form-control college-search-bar" placeholder="Search by name or location">
    <div class="row" id="college-cards"></div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>

<script>
    document.addEventListener('DOMContentLoaded', () => {
        const collegeCardsContainer = document.getElementById('college-cards');
        const searchBar = document.getElementById('search-bar');
        const placeholderImageUrl = 'https://www.avantistones.com/images/noImage.png';
        let collegesData = [];
        
        async function fetchData() {
            try {
                const response = await fetch('https://collegerankings.stu.nighthawkcodingsociety.com/api/college/colleges');
                const data = await response.json();
                collegesData = data;
                renderColleges(collegesData);
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }
        
        function renderColleges(colleges) {
            collegeCardsContainer.innerHTML = '';
            colleges.forEach(college => {
                const collegeCard = document.createElement('div');
                collegeCard.classList.add('col-lg-4', 'col-md-6', 'mb-4');
                collegeCard.innerHTML = `
                    <div class="card">
                        <img src="${college.image || placeholderImageUrl}" class="card-img-top" alt="${college.name}">
                        <div class="card-body">
                            <h5 class="card-title">${college.name}</h5>
                            <p class="card-text">${college.city}, ${college.state}</p>
                            <p class="card-text">Ranking: ${college.ranking || 'Not Available'}</p>
                            <button data-college-id="${college.id}" class="btn btn-primary view-details-btn">View Details</button>
                        </div>
                    </div>
                `;
                collegeCardsContainer.appendChild(collegeCard);
            });
            
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
        }
        
        function filterColleges() {
            const searchTerm = searchBar.value.toLowerCase();
            const filteredColleges = collegesData.filter(college => {
                const collegeName = college.name.toLowerCase();
                const collegeLocation = `${college.city}, ${college.state}`.toLowerCase();
                return collegeName.includes(searchTerm) || collegeLocation.includes(searchTerm);
            });
            renderColleges(filteredColleges);
        }
        
        fetchData();
        searchBar.addEventListener('input', filterColleges);
    });
</script>

</body>
</html>
