# PRODIGY_TrackCode_02
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Stopwatch App</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to right, #4b0082, #6a5acd);
            color: white;
            text-align: center;
            margin-top: 100px;
        }

        h1 {
            font-size: 40px;
        }

        #display {
            font-size: 50px;
            margin: 20px 0;
        }

        button {
            padding: 10px 20px;
            font-size: 18px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .start { background-color: green; color: white; }
        .pause { background-color: orange; color: white; }
        .reset { background-color: red; color: white; }
        .lap   { background-color: blue; color: white; }

        ul {
            list-style: none;
            padding: 0;
        }
    </style>
</head>

<body>

    <h1>Stopwatch</h1>

    <div id="display">00:00:00</div>

    <button class="start" onclick="start()">Start</button>
    <button class="pause" onclick="pause()">Pause</button>
    <button class="reset" onclick="reset()">Reset</button>
    <button class="lap" onclick="lap()">Lap</button>

    <h2>Lap Times</h2>
    <ul id="laps"></ul>

    <script>
        let seconds = 0;
        let minutes = 0;
        let hours = 0;
        let timer = null;

        function updateDisplay() {
            let h = hours < 10 ? "0" + hours : hours;
            let m = minutes < 10 ? "0" + minutes : minutes;
            let s = seconds < 10 ? "0" + seconds : seconds;

            document.getElementById("display").innerText = h + ":" + m + ":" + s;
        }

        function stopwatch() {
            seconds++;

            if (seconds == 60) {
                seconds = 0;
                minutes++;
            }

            if (minutes == 60) {
                minutes = 0;
                hours++;
            }

            updateDisplay();
        }

        function start() {
            if (timer !== null) return;
            timer = setInterval(stopwatch, 1000);
        }

        function pause() {
            clearInterval(timer);
            timer = null;
        }

        function reset() {
            clearInterval(timer);
            timer = null;
            seconds = 0;
            minutes = 0;
            hours = 0;
            updateDisplay();
            document.getElementById("laps").innerHTML = "";
        }

        function lap() {
            let li = document.createElement("li");
            li.innerText = document.getElementById("display").innerText;
            document.getElementById("laps").appendChild(li);
        }
    </script>

</body>
</html>
