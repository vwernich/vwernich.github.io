<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pulsing Button Page</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f0f0f0;
            overflow: hidden;
            position: relative;
            font-family: Arial, sans-serif;
        }

        .button {
            background-color: #ff4f84;
            color: white;
            padding: 20px 40px;
            font-size: 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            animation: pulse 1.5s infinite;
            transition: opacity 0.5s ease;
        }

        @keyframes pulse {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.1); opacity: 0.8; }
            100% { transform: scale(1); opacity: 1; }
        }

        .exit-button {
            position: absolute;
            top: 20px;
            right: 20px;
            padding: 10px 20px;
            background-color: #333;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            display: none;
        }

        .message {
            position: absolute;
            font-size: 30px;
            font-weight: bold;
            color: #333;
            user-select: none;
            animation: floatMessage 10s ease-in-out infinite;
        }

        @keyframes floatMessage {
            0% { transform: translateY(0); opacity: 1; }
            50% { transform: translateY(-20px); opacity: 0.5; }
            100% { transform: translateY(0); opacity: 1; }
        }

        .background {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: url('dancing-gif-1.gif');
            background-size: cover;
            background-position: center;
            opacity: 0.3;
            z-index: -1;
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="background"></div>
    <button class="button" id="pushMeBtn">Push me</button>
    <button class="exit-button" id="exitBtn">Exit</button>

    <script>
        const pushMeBtn = document.getElementById('pushMeBtn');
        const exitBtn = document.getElementById('exitBtn');
        const body = document.body;

        pushMeBtn.addEventListener('click', () => {
            pushMeBtn.classList.add('hidden');
            exitBtn.classList.remove('hidden');
            displayMessages();
        });

        exitBtn.addEventListener('click', () => {
            exitBtn.classList.add('hidden');
            pushMeBtn.classList.remove('hidden');
            removeMessages();
        });

        function displayMessages() {
            for (let i = 0; i < 20; i++) {
                const message = document.createElement('div');
                message.classList.add('message');
                message.style.top = `${Math.random() * 100}vh`;
                message.style.left = `${Math.random() * 100}vw`;
                message.textContent = "Hello Chandre";
                body.appendChild(message);
            }
        }

        function removeMessages() {
            const messages = document.querySelectorAll('.message');
            messages.forEach(msg => msg.remove());
        }
    </script>
</body>
</html>
