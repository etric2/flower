<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Choose Yes or No</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f7f7f7;
            margin: 0;
            overflow: hidden;
            position: relative;
        }
        .message {
            position: fixed;
            top: 50px;
            left: 0;
            right: 0;
            text-align: center;
            font-size: 24px;
            font-weight: bold;
            color: #ff69b4;
            opacity: 0;
            transition: opacity 0.5s;
            z-index: 100;
        }
        .button-container {
            display: flex;
            gap: 20px;
            margin-top: 20px;
        }
        .btn {
            padding: 12px 24px;
            font-size: 18px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .btn-yes {
            background-color: #4CAF50;
            color: white;
        }
        .btn-no {
            background-color: #f44336;
            color: white;
        }
        .btn:hover {
            transform: scale(1.05);
        }
        .flower-container {
            position: absolute;
            width: 100%;
            height: 100%;
            display: none;
            justify-content: center;
            align-items: center;
            z-index: -1;
        }
        .flower {
            position: relative;
            width: 200px;
            height: 200px;
        }
        .petal {
            position: absolute;
            width: 70px;
            height: 70px;
            background-color: #ff69b4;
            border-radius: 50%;
        }
        .center {
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: #ffd700;
            border-radius: 50%;
            top: 75px;
            left: 75px;
        }
        .stem {
            position: absolute;
            width: 10px;
            height: 150px;
            background-color: #4CAF50;
            top: 150px;
            left: 95px;
        }
        .leaf {
            position: absolute;
            width: 40px;
            height: 20px;
            background-color: #4CAF50;
            border-radius: 40px 0;
            transform: rotate(45deg);
            top: 200px;
            left: 90px;
        }
    </style>
</head>
<body>
    <div class="message" id="message">I love you so muchh, mwaaa</div>
    <div class="button-container">
        <button class="btn btn-yes" id="yesBtn">Yes</button>
        <button class="btn btn-no" id="noBtn">No</button>
    </div>
    <div class="flower-container" id="flowerContainer">
        <div class="flower">
            <div class="petal" style="top: 0; left: 65px;"></div>
            <div class="petal" style="top: 65px; left: 0;"></div>
            <div class="petal" style="top: 65px; left: 130px;"></div>
            <div class="petal" style="top: 130px; left: 65px;"></div>
            <div class="petal" style="top: 20px; left: 20px;"></div>
            <div class="petal" style="top: 20px; left: 110px;"></div>
            <div class="petal" style="top: 110px; left: 20px;"></div>
            <div class="petal" style="top: 110px; left: 110px;"></div>
            <div class="center"></div>
            <div class="stem"></div>
            <div class="leaf"></div>
        </div>
    </div>
    <script>
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const message = document.getElementById('message');
        const flowerContainer = document.getElementById('flowerContainer');  
        let yesBtnSize = 1;
        yesBtn.addEventListener('click', function() {
            // Show the message
            message.style.opacity = '1';   
            // Show the flower
            flowerContainer.style.display = 'flex';   
            // Hide the buttons
            yesBtn.style.display = 'none';
            noBtn.style.display = 'none';   
            // Set a timeout to hide the message after 5 seconds
            setTimeout(() => {
                message.style.opacity = '0';
            }, 5000);
        });
        noBtn.addEventListener('click', function() {
            // Increase the yes button size
            yesBtnSize += 0.4;
            // Apply the new size
            yesBtn.style.transform = `scale(${yesBtnSize})`;    
            // Make the yes button more noticeable
            yesBtn.style.boxShadow = '0 0 20px rgba(255, 105, 180, 0.8)';
            yesBtn.style.zIndex = '10';  
            // If the yes button gets too big, make the no button smaller
            if (yesBtnSize > 2) {
                noBtn.style.transform = 'scale(0.8)';
            }   
            // If the yes button gets even bigger, make the no button even smaller
            if (yesBtnSize > 3) {
                noBtn.style.transform = 'scale(0.6)';
            }  
            // If the yes button gets extremely big, almost hide the no button
            if (yesBtnSize > 4) {
                noBtn.style.transform = 'scale(0.3)';
                noBtn.style.opacity = '0.5';
            }   
            // Add some animation to make it playful
            yesBtn.animate([
                { transform: `scale(${yesBtnSize - 0.2})` },
                { transform: `scale(${yesBtnSize})` }
            ], {
                duration: 300,
                easing: 'ease-out'
            });
        });
        // Add some extra flowers when yes is clicked
        yesBtn.addEventListener('click', function() {
            for (let i = 0; i < 10; i++) {
                setTimeout(() => {
                    createRandomFlower();
                }, i * 300);
            }
        });
        function createRandomFlower() {
            const flower = document.createElement('div');
            flower.className = 'flower';
            flower.style.position = 'absolute';
            flower.style.left = Math.random() * 90 + 'vw';
            flower.style.top = Math.random() * 90 + 'vh';
            flower.style.transform = 'scale(' + (Math.random() * 0.5 + 0.5) + ')';
            // Create flower parts
            const colors = ['#ff69b4', '#ff9ed2', '#ffb6c1', '#ffc0cb'];
            for (let i = 0; i < 8; i++) {
                const petal = document.createElement('div');
                petal.className = 'petal';
                const angle = i * 45;
                const radius = 35;
                const x = Math.cos(angle * Math.PI / 180) * radius + 35;
                const y = Math.sin(angle * Math.PI / 180) * radius + 35;
                petal.style.left = x + 'px';
                petal.style.top = y + 'px';
                petal.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                flower.appendChild(petal);
            }
            const center = document.createElement('div');
            center.className = 'center';
            flower.appendChild(center);
            flowerContainer.appendChild(flower);
            // Add animation
            flower.animate([
                { opacity: 0, transform: 'scale(0.2)' },
                { opacity: 1, transform: 'scale(' + (Math.random() * 0.5 + 0.5) + ')' }
            ], {
                duration: 1000,
                easing: 'ease-out'
            });
        }
    </script>
</body>
</html>
