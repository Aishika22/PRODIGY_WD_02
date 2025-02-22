<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        #stopwatch {
            font-size: 2em;
            margin-bottom: 20px;
        }
        button {
            font-size: 1em;
            margin: 5px;
            padding: 10px;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
    </style>
</head>
<body>
    <div id="stopwatch">00:00:00</div>
    <button onclick="startStopwatch()">Start</button>
    <button onclick="pauseStopwatch()">Pause</button>
    <button onclick="resetStopwatch()">Reset</button>
    <button onclick="lapTime()">Lap</button>
    <ul id="laps"></ul>

    <script>
        let timer;
        let isRunning = false;
        let seconds = 0, minutes = 0, hours = 0;
        
        function updateDisplay() {
            const formattedTime = 
                (hours < 10 ? '0' + hours : hours) + ':' +
                (minutes < 10 ? '0' + minutes : minutes) + ':' +
                (seconds < 10 ? '0' + seconds : seconds);
            document.getElementById('stopwatch').textContent = formattedTime;
        }

        function startStopwatch() {
            if (!isRunning) {
                isRunning = true;
                timer = setInterval(() => {
                    seconds++;
                    if (seconds === 60) {
                        seconds = 0;
                        minutes++;
                    }
                    if (minutes === 60) {
                        minutes = 0;
                        hours++;
                    }
                    updateDisplay();
                }, 1000);
            }
        }

        function pauseStopwatch() {
            clearInterval(timer);
            isRunning = false;
        }

        function resetStopwatch() {
            clearInterval(timer);
            isRunning = false;
            seconds = 0;
            minutes = 0;
            hours = 0;
            updateDisplay();
            document.getElementById('laps').innerHTML = '';
        }

        function lapTime() {
            if (isRunning) {
                const lapRecord = document.createElement('li');
                lapRecord.textContent = document.getElementById('stopwatch').textContent;
                document.getElementById('laps').appendChild(lapRecord);
            }
        }
    </script>
</body>
</html>
