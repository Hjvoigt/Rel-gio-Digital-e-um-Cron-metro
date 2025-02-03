<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relógio Digital e Cronômetro</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #282c34;
            color: white;
            margin: 50px;
            overflow: hidden;
        }
        .container {
            max-width: 400px;
            margin: auto;
            padding: 20px;
            background: #444;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }
        #clock {
            font-size: 2em;
            margin-bottom: 20px;
        }
        #stopwatch {
            font-size: 2em;
        }
        .buttons button {
            margin: 5px;
            padding: 10px 20px;
            font-size: 1em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .start { background: green; color: white; }
        .pause { background: orange; color: white; }
        .reset { background: red; color: white; }
        .theme-toggle {
            margin-top: 20px;
            padding: 10px;
            font-size: 1em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background: #ccc;
            color: black;
        }
        .light-mode {
            background-color: white;
            color: black;
        }
        .light-mode .container {
            background: #f0f0f0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Relógio Digital</h1>
        <div id="clock"></div>
        
        <h1>Cronômetro</h1>
        <div id="stopwatch">00:00:00</div>
        <div class="buttons">
            <button class="start" onclick="startStopwatch()">Iniciar</button>
            <button class="pause" onclick="pauseStopwatch()">Pausar</button>
            <button class="reset" onclick="resetStopwatch()">Zerar</button>
        </div>
        <button class="theme-toggle" onclick="toggleTheme()">Modo Claro</button>
    </div>
    <script>
        function updateClock() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            document.getElementById('clock').textContent = `${hours}:${minutes}:${seconds}`;
        }
        setInterval(updateClock, 1000);
        updateClock();

        let stopwatchInterval;
        let elapsedSeconds = 0;
        let isRunning = false;

        function updateStopwatch() {
            const hours = String(Math.floor(elapsedSeconds / 3600)).padStart(2, '0');
            const minutes = String(Math.floor((elapsedSeconds % 3600) / 60)).padStart(2, '0');
            const seconds = String(elapsedSeconds % 60).padStart(2, '0');
            document.getElementById('stopwatch').textContent = `${hours}:${minutes}:${seconds}`;
        }

        function startStopwatch() {
            if (!isRunning) {
                isRunning = true;
                stopwatchInterval = setInterval(() => {
                    elapsedSeconds++;
                    updateStopwatch();
                }, 1000);
            }
        }

        function pauseStopwatch() {
            clearInterval(stopwatchInterval);
            isRunning = false;
        }

        function resetStopwatch() {
            clearInterval(stopwatchInterval);
            elapsedSeconds = 0;
            isRunning = false;
            updateStopwatch();
        }

        function toggleTheme() {
            document.body.classList.toggle("light-mode");
            const button = document.querySelector(".theme-toggle");
            if (document.body.classList.contains("light-mode")) {
                button.textContent = "Modo Escuro";
            } else {
                button.textContent = "Modo Claro";
            }
        }
    </script>
</body>
</html>
