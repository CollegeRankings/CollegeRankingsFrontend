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
        }
        h1 {
            color: #333;
        }
        p {
            color: #666;
        }
        img {
            width: 100%;
            height: auto;
            margin-bottom: 15px;
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
            console.log(collegeId)
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
                        <p><strong>Type:</strong> ${college.type}</p>
                        <p><strong>Ranking:</strong> ${college.ranking}</p>
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
                    `;
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
