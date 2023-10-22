---
permalink: /colleges/college_details
title: College Details
---

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>College Info</title>
    <style>
        /* Your existing styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f8f8;
            margin: 0;
            padding: 0;
        }
        .college-info {
            background-color: #fff;
            margin: 20px;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: #333;
            font-size: 24px;
            margin-bottom: 10px;
        }
        p {
            color: #666;
            margin-bottom: 5px;
        }
        img {
            width: 60%; /* Decreased image width to 60% of its parent container */
            height: auto;
            margin-bottom: 15px;
            border-radius: 8px;
        }
        a {
            color: #3498db;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        /* Additional Styles */
        .college-details {
            margin-top: 20px;
        }
        .college-details p {
            font-size: 16px;
            margin-bottom: 8px;
        }
        .college-details strong {
            color: #333;
        }
    </style>
</head>

<body>
    <div class="college-info" id="college-info">
        <!-- College information will be inserted here dynamically using JavaScript -->
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const urlParams = new URLSearchParams(window.location.search);
            const collegeId = urlParams.get('id');
            const collegeInfoContainer = document.getElementById('college-info');
            async function fetchCollegeInfo() {
                try {
                    const response = await fetch(`https://collegerankings.stu.nighthawkcodingsociety.com/api/college/collegedetails?id=${collegeId}`);
                    console.log(response)
                    const college = await response.json();
                    collegeInfoContainer.innerHTML = `
                        <img src="${college.image}" alt="${college.name}" />
                        <h1>${college.name}</h1>
                        <p><strong>State:</strong> ${college.state}</p>
                        <p><strong>City:</strong> ${college.city}</p>
                        <p><strong>Zip Code:</strong> ${college.zip}</p>
                        <div class="college-details">
                            <p><strong>Type:</strong> ${college.type}</p>
                            <p><strong>Ranking:</strong> <span id="rankingValue">${college.ranking}</span> <button id="toggleBinaryBtn" class="btn btn-secondary">Show Ranking as Binary</button></p>
                            <p><strong>ACT Average:</strong> ${college.ACTAvg}</p>
                            <p><strong>Aid Percentage:</strong> ${college.aidpercent}%</p>
                            <p><strong>Acceptance Rate:</strong> ${college.acceptance}%</p>
                            <p><strong>Fees:</strong> $${college.fees}</p>
                            <p><strong>GPA Average:</strong> ${college.GPAAvg}</p>
                            <p><strong>Enrollment:</strong> ${college.enrollment}</p>
                            <p><strong>SAT Average:</strong> ${college.SATAvg}</p>
                            <p><strong>SAT Range:</strong> ${college.SATRange}</p>
                            <p><strong>ACT Range:</strong> ${college.ACTRange}</p>
                            <p><strong>Year Founded:</strong> ${college.YearFounded}</p>
                            <p><strong>Academic Calendar:</strong> ${college.AcademicCalendar}</p>
                            <p><strong>Setting:</strong> ${college.setting}</p>
                            <p><strong>School Website:</strong> <a href="${college.SchoolWebsite}" target="_blank">Visit Website</a></p>
                        </div>
                    `;
                    // Add click event handler for the "Toggle Binary" button
                    const rankingValue = document.getElementById('rankingValue');
                    const toggleBinaryBtn = document.getElementById('toggleBinaryBtn');
                    toggleBinaryBtn.addEventListener('click', () => {
                        // Convert the ranking to binary
                        const binaryRank = (parseInt(college.ranking) || 0).toString(2);
                        // Display both the actual ranking and the binary ranking together
                        rankingValue.textContent = `${college.ranking} (Binary: ${binaryRank})`;
                    });
                } catch (error) {
                    console.error('Error fetching data:', error);
                    collegeInfoContainer.innerHTML = '<p>Error loading college information.</p>';
                }
            }
            fetchCollegeInfo();
        });
    </script>
</body>

</html>
