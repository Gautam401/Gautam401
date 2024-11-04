<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Date and Time Duration Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #e0f7fa; /* Light blue background */
            color: #333;
        }
        .hidden {
            display: none;
        }
        h1 {
            text-align: center;
            color: #00796b;
        }
        label, select, input, button {
            display: block;
            width: 100%;
            margin: 10px 0;
            padding: 10px;
            font-size: 1rem;
        }
        select, input, button {
            border: none;
            border-radius: 8px;
            box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.2);
            background-color: #ffffff;
        }
        button {
            background-color: #00796b;
            color: #ffffff;
            cursor: pointer;
        }
        button:hover {
            background-color: #004d40;
        }
        #inputFields {
            max-width: 400px;
            margin: 0 auto;
            background-color: #ffffff;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 2px 2px 12px rgba(0, 0, 0, 0.2);
        }
        #result {
            max-width: 400px;
            margin: 20px auto;
            padding: 20px;
            background-color: #ffffff;
            border-radius: 12px;
            box-shadow: 2px 2px 12px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body>
    <h1>Date and Time Duration Calculator</h1>
    <label for="selection">Choose an option:</label>
    <select id="selection" onchange="showInputField()">
        <option value="">--Select--</option>
        <option value="duration">Calculate Duration</option>
    </select>

    <div id="inputFields" class="hidden">
        <label for="startDate">Enter Start Date (DD/MM/YYYY):</label>
        <input type="text" id="startDate" placeholder="15/01/2012">
        <label for="startTime">Enter Start Time (HH:MM:SS):</label>
        <input type="text" id="startTime" placeholder="14:30:00">
        <label for="endDate">Enter End Date (DD/MM/YYYY):</label>
        <input type="text" id="endDate" placeholder="16/08/2020">
        <label for="endTime">Enter End Time (HH:MM:SS):</label>
        <input type="text" id="endTime" placeholder="15:45:00">
        <button onclick="calculateDuration()">Calculate</button>
    </div>

    <h2 id="result" class="hidden"></h2>

    <script>
        function showInputField() {
            const selection = document.getElementById("selection").value;
            const inputFields = document.getElementById("inputFields");
            const result = document.getElementById("result");

            if (selection === "duration") {
                inputFields.classList.remove("hidden");
                result.classList.add("hidden");
            }
        }

        function isLeapYear(year) {
            return (year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0);
        }

        function calculateDuration() {
            const startDateInput = document.getElementById("startDate").value;
            const startTimeInput = document.getElementById("startTime").value;
            const endDateInput = document.getElementById("endDate").value;
            const endTimeInput = document.getElementById("endTime").value;

            const [day1, month1, year1] = startDateInput.split('/').map(Number);
            const [hour1, minute1, second1] = startTimeInput.split(':').map(Number);
            const [day2, month2, year2] = endDateInput.split('/').map(Number);
            const [hour2, minute2, second2] = endTimeInput.split(':').map(Number);

            const startDate = new Date(year1, month1 - 1, day1, hour1, minute1, second1);
            const endDate = new Date(year2, month2 - 1, day2, hour2, minute2, second2);

            // Calculate time difference
            const timeDifference = endDate - startDate;

            // Calculate total duration
            const totalDays = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
            const totalWeeks = Math.floor(totalDays / 7);
            const remainingDays = totalDays % 7;

            const totalMonths = ((endDate.getFullYear() - startDate.getFullYear()) * 12) + (endDate.getMonth() - startDate.getMonth());
            const remainingMonths = totalMonths % 12;
            const totalYears = endDate.getFullYear() - startDate.getFullYear();
            const totalCompleteYears = Math.floor(totalMonths / 12);

            // Calculate remaining time components
            const totalSeconds = Math.floor(timeDifference / 1000);
            const totalMinutes = Math.floor(totalSeconds / 60);
            const totalHours = Math.floor(totalMinutes / 60);
            const remainingHours = totalHours % 24;
            const remainingMinutes = totalMinutes % 60;
            const remainingSeconds = totalSeconds % 60;

            // Get the day of the week for both dates
            const daysOfWeek = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            const startDayOfWeek = daysOfWeek[startDate.getDay()];
            const endDayOfWeek = daysOfWeek[endDate.getDay()];

            // Calculate leap years
            let leapYears = [];
            for (let year = year1; year <= year2; year++) {
                if (isLeapYear(year)) {
                    leapYears.push(year);
                }
            }

            // Display results
            const result = document.getElementById("result");
            result.innerHTML = `
                <strong>Total Duration:</strong><br>
                Total Years: ${totalCompleteYears} Years<br>
                Remaining Months: ${remainingMonths} Months<br>
                Total Weeks: ${totalWeeks} Weeks<br>
                Remaining Days: ${remainingDays} Days<br>
                Total Hours: ${remainingHours} Hours<br>
                Remaining Minutes: ${remainingMinutes} Minutes<br>
                Remaining Seconds: ${remainingSeconds} Seconds<br>
                <strong>Day of the Week:</strong><br>
                Start Date (${startDateInput} ${startTimeInput}) is a ${startDayOfWeek}.<br>
                End Date (${endDateInput} ${endTimeInput}) is a ${endDayOfWeek}.<br>
                <strong>Leap Years:</strong><br>
                Total Leap Years: ${leapYears.length}<br>
                ${leapYears.length > 0 ? "Leap Years: " + leapYears.join(", ") : "No leap years in this period."}
            `;
            result.classList.remove("hidden");
        }
    </script>
</body>
</html>
