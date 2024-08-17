<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        body {
            font-family: 'Helvetica Neue', Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
            margin: 0;
            color: #333;
            display: flex;
            justify-content: space-between;
            height: 100vh;
        }

        .left-container {
            width: 70%;
        }

        .right-container {
            width: 25%;
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .text-container {
            background-color: #ffffff;
            padding: 15px;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            white-space: pre-wrap;
            position: relative;
            margin-top: 20px;
            height: 60vh;
            overflow-y: auto;
        }

        h1 {
            color: #1171ba;
            text-align: center;
            margin-bottom: 30px;
            font-size: 28px;
        }

        .reminder-header {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .current-time {
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .time-slot {
            width: 100%;
            padding: 10px;
            border: 1px solid #1171ba;
            border-radius: 5px;
            cursor: pointer;
            margin-bottom: 10px;
            transition: background-color 0.3s;
            text-align: center;
        }

        .time-slot:hover {
            background-color: #e0f4ff;
        }

        .time-slot.selected {
            background-color: #1171ba;
            color: white;
        }

        .popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            display: none;
            z-index: 100;
        }

        .popup button {
            background-color: #1171ba;
            border: none;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            margin-top: 10px;
        }

        .popup button:hover {
            background-color: #0e619f;
        }

        .hidden {
            display: none;
        }
    </style>
</head>

<body>
    <div class="left-container">
        <h1>Advertisements-PPH</h1>

        <!-- Placeholder for the text processing area -->
        <div id="output" class="text-container">
            <p id="cursorStart">Place your cursor here</p>
            <!-- Result box content goes here -->
        </div>
    </div>

    <div class="right-container">
        <div class="reminder-header">Ad Slots Reminder</div>
        <div id="currentTime" class="current-time">--:--:--</div>
        <div id="slotsContainer"></div>
    </div>

    <div id="popup" class="popup">
        <p>Send Ads</p>
        <button onclick="dismissPopup()">OK</button>
    </div>

    <script>
        const slots = [
            "9:00-9:30am", "10:35-10:45am", "11:50-12:00pm",
            "1:05-1:10pm", "2:20-2:30pm", "3:40-3:45pm", "4:50-5:00pm"
        ];

        const slotTimes = {
            "9:00-9:30am": "09:00",
            "10:35-10:45am": "10:35",
            "11:50-12:00pm": "11:50",
            "1:05-1:10pm": "13:05",
            "2:20-2:30pm": "14:20",
            "3:40-3:45pm": "15:40",
            "4:50-5:00pm": "16:50"
        };

        const slotsContainer = document.getElementById('slotsContainer');
        const reminders = {};

        function updateCurrentTime() {
            const now = new Date();
            const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' });
            document.getElementById('currentTime').textContent = timeString;

            const currentHourMinute = now.toTimeString().slice(0, 5);
            if (reminders[currentHourMinute]) {
                showPopup();
                reminders[currentHourMinute] = false; // Remove the reminder after triggering
            }
        }

        function showPopup() {
            const popup = document.getElementById('popup');
            popup.style.display = 'block';
            if (document.hidden) {
                document.title = "⚠ Reminder!";
            }
        }

        function dismissPopup() {
            const popup = document.getElementById('popup');
            popup.style.display = 'none';
            document.title = "Advertisements-PPH";
        }

        function setReminder(timeSlot) {
            const slotElement = document.getElementById(timeSlot);
            if (!slotElement.classList.contains('selected')) {
                slotElement.classList.add('selected');
                const reminderTime = slotTimes[timeSlot];
                reminders[reminderTime] = true;
            } else {
                slotElement.classList.remove('selected');
                const reminderTime = slotTimes[timeSlot];
                reminders[reminderTime] = false;
            }
        }

        function renderSlots() {
            slots.forEach(slot => {
                const slotElement = document.createElement('div');
                slotElement.id = slot;
                slotElement.className = 'time-slot';
                slotElement.textContent = slot;
                slotElement.onclick = () => setReminder(slot);
                slotsContainer.appendChild(slotElement);
            });
        }

        renderSlots();
        setInterval(updateCurrentTime, 1000);

        // Tab visibility change event to make the tab title blink
        document.addEventListener("visibilitychange", function() {
            if (!document.hidden && document.title === "⚠ Reminder!") {
                document.title = "Advertisements-PPH";
            }
        });
    </script>
</body>

</html>
