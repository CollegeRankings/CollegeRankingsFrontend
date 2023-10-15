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
        body {
            background-color: #f8f9fa;
            font-family: 'Arial', sans-serif;
        }
        .container {
            margin-top: 50px;
        }
        h1 {
            color: #495057;
            margin-bottom: 20px;
        }
        #search-bar {
            margin-bottom: 20px;
        }
        .card {
            transition: transform 0.3s ease-in-out;
        }
        .card:hover {
            transform: scale(1.05);
        }
        .card-img-top {
            height: 200px;
            object-fit: cover;
        }
        .card-title, .card-text {
            color: #495057;
        }
        @media (max-width: 768px) {
            h1 {
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>College Search</h1>
        <input type="text" id="search-bar" class="form-control" placeholder="Search by name or location">
        <br>
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
                        location.href = `college_details?id=${collegeId}`;
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
