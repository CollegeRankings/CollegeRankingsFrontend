---
permalink: /colleges
title: Plans
---

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Colleges</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>
</head>
<body>
    <div class="container">
        <h1>College Search</h1>
        <input type="text" id="search-bar" class="form-control" placeholder="Search by name or location">
        <br>
        <div class="row" id="college-cards"></div>
    </div>
    <script>
        const collegeCardsContainer = document.getElementById("college-cards");
        const searchBar = document.getElementById("search-bar");
        const placeholderImageUrl = "https://www.avantistones.com/images/noImage.png";
        let collegesData = []; // Stores the original data
        // Fetch JSON data from the local server
        fetch('https://collegerankings.stu.nighthawkcodingsociety.com/api/college/colleges')
            .then(response => response.json())
            .then(data => {
                collegesData = data; // Store the original data
                renderColleges(collegesData); // Display all colleges initially
            })
            .catch(error => console.error('Error fetching data:', error));
        // Add event listener for the search bar
        searchBar.addEventListener('input', filterColleges);
        function renderColleges(colleges) {
            collegeCardsContainer.innerHTML = ""; // Clear existing cards
            colleges.forEach(college => {
                const collegeCard = document.createElement("div");
                collegeCard.classList.add("col-lg-4", "col-md-6", "mb-4");
                collegeCard.innerHTML = `
                    <div class="card">
                        <img src="${college.image || placeholderImageUrl}" class="card-img-top" alt="${college.name}">
                        <div class="card-body">
                            <h5 class="card-title">${college.name}</h5>
                            <p class="card-text">${college.city}, ${college.state}</p>
                            <p class="card-text">Ranking: ${college.ranking || 'Not Available'}</p>
                        </div>
                    </div>
                `;
                collegeCardsContainer.appendChild(collegeCard);
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
    </script>
</body>

</html>