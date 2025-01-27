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
        }

        .left-side {
            left: 10vw;
            top: 50%;
            transform: translateY(-50%);
        }

        .right-side {
            right: 10vw;
            top: 50%;
            transform: translateY(-50%);
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

        .firework {
            position: absolute;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            animation: firework 1s ease-out infinite;
        }

        @keyframes firework {
            0% {
                transform: scale(1) translate(0, 0);
                opacity: 1;
            }
            100% {
                transform: scale(1) translate(var(--x), var(--y));
                opacity: 0;
            }
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
            // Create "Hello Chandre" on the left side
            const leftMessage = document.createElement('div');
            leftMessage.classList.add('message', 'left-side');
            leftMessage.textContent = "Hello Chandre";
            body.appendChild(leftMessage);
            
            // Create fireworks from the left message
            createFireworks(leftMessage, 'left');

            // Create "Hello Chandre" on the right side
            const rightMessage = document.createElement('div');
            rightMessage.classList.add('message', 'right-side');
            rightMessage.textContent = "Hello Chandre";
            body.appendChild(rightMessage);
            
            // Create fireworks from the right message
            createFireworks(rightMessage, 'right');
        }

        function removeMessages() {
            const messages = document.querySelectorAll('.message');
            messages.forEach(msg => msg.remove());
            const fireworks = document.querySelectorAll('.firework');
            fireworks.forEach(fw => fw.remove());
        }

        function createFireworks(message, side) {
            const fireworkCount = 20;
            const maxDistance = 120;
            const messageRect = message.getBoundingClientRect();
            const centerX = messageRect.left + messageRect.width / 2;
            const centerY = messageRect.top + messageRect.height / 2;

            // Create fireworks particles
            for (let i = 0; i < fireworkCount; i++) {
                const firework = document.createElement('div');
                firework.classList.add('firework');
                body.appendChild(firework);

                // Randomly generate a color
                firework.style.backgroundColor = getRandomColor();

                // Calculate random distance and direction
                const angle = Math.random() * Math.PI * 2;
                const distance = Math.random() * maxDistance;
                const xOffset = Math.cos(angle) * distance;
                const yOffset = Math.sin(angle) * distance;

                // Position the fireworks at the message center and animate them outward
                firework.style.left = `${centerX}px`;
                firework.style.top = `${centerY}px`;

                // Use CSS custom properties to define the movement (to be used in the animation)
                firework.style.setProperty('--x', `${xOffset}px`);
                firework.style.setProperty('--y', `${yOffset}px`);
            }
        }

        // Function to generate random color for fireworks
        function getRandomColor() {
            const letters = '0123456789ABCDEF';
            let color = '#';
            for (let i = 0; i < 6; i++) {
                color += letters[Math.floor(Math.random() * 16)];
            }
            return color;
        }
    </script>
</body>
</html>
