<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>67 OUSSA</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .chronometre {
            text-align: center;
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .time {
            font-size: 48px;
            margin-bottom: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            margin: 5px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
        }
        #startPause {
            background-color: #4CAF50;
            color: white;
        }
        #reset {
            background-color: #f44336;
            color: white;
        }
    </style>
</head>
<body>

    <div class="chronometre">
        <div class="time" id="display">00:00</div>
        <button id="startPause">Démarrer</button>
        <button id="reset">Réinitialiser</button>
    </div>

    <script>
        let startTime = 0;
        let running = false;
        let interval;
        let totalTime = 0; // Temps total depuis le démarrage ou la dernière reprise

        function formatTime(seconds) {
            const minutes = Math.floor(seconds / 60);
            const secs = seconds % 60;
            return `${String(minutes).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
        }

        function updateTime() {
            totalTime++;
            document.getElementById('display').textContent = formatTime(totalTime);
        }

        document.getElementById('startPause').addEventListener('click', function() {
            if (running) {
                clearInterval(interval);
                this.textContent = 'Démarrer';
            } else {
                interval = setInterval(updateTime, 1000);
                this.textContent = 'Pause';
            }
            running = !running;
        });

        document.getElementById('reset').addEventListener('click', function() {
            clearInterval(interval);
            running = false;
            totalTime = 0;
            document.getElementById('display').textContent = '00:00';
            document.getElementById('startPause').textContent = 'Démarrer';
        });
    </script>

</body>
</html>
