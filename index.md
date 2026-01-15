<!DOCTYPE md>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Draggable Animated Circles</title>
    <style>
        body {
            margin: 0;
            padding: 50px;
            min-height: 100vh;
            background: #f0f0f0;
            font-family: Arial, sans-serif;
            overflow: hidden;
            user-select: none;
        }
        
        #circlesContainer {
            position: absolute;
            cursor: grab;
            z-index: 1000;
        }
        
        #circlesContainer:active {
            cursor: grabbing;
        }
        
        .circle {
            display: inline-block;
            width: 2in;  /* 1in radius = 2in diameter */
            height: 2in;
            border-radius: 50%;
            border: 3px solid #333;
            margin: 0 25px;
        }
        
        #circle1 {
            background: #ff4444;
            animation: changeColor1 3s infinite;
        }
        
        #circle2 {
            background: #44ff44;
            animation: changeColor2 1s infinite;
        }
        
        #circle3 {
            background: #4444ff;
            animation: changeColor3 7s infinite;
        }
        
        @keyframes changeColor1 {
            0%, 33% { background: #ff4444; }
            33.1%, 66% { background: #44ff44; }
            66.1%, 100% { background: #4444ff; }
        }
        
        @keyframes changeColor2 {
            0%, 33% { background: #44ff44; }
            33.1%, 66% { background: #4444ff; }
            66.1%, 100% { background: #ff4444; }
        }
        
        @keyframes changeColor3 {
            0%, 14% { background: #4444ff; }
            14.1%, 28% { background: #ff4444; }
            28.1%, 42% { background: #44ff44; }
            42.1%, 100% { background: #4444ff; }
        }
    </style>
</head>
<body>
    <div id="circlesContainer">
        <div id="circle1" class="circle" title="3s cycle"></div>
        <div id="circle2" class="circle" title="1s cycle"></div>
        <div id="circle3" class="circle" title="7s cycle"></div>
    </div>

    <script>
        const container = document.getElementById('circlesContainer');
        let isDragging = false;
        let currentX;
        let currentY;
        let initialX;
        let initialY;
        let xOffset = 0;
        let yOffset = 0;

        container.addEventListener('mousedown', startDragging);
        document.addEventListener('mousemove', drag);
        document.addEventListener('mouseup', stopDragging);

        function startDragging(e) {
            initialX = e.clientX - xOffset;
            initialY = e.clientY - yOffset;

            if (e.target === container || container.contains(e.target)) {
                isDragging = true;
            }
        }

        function drag(e) {
            if (isDragging) {
                e.preventDefault();
                currentX = e.clientX - initialX;
                currentY = e.clientY - initialY;

                xOffset = currentX;
                yOffset = currentY;

                container.style.transform = `translate(${currentX}px, ${currentY}px)`;
            }
        }

        function stopDragging() {
            isDragging = false;
        }
    </script>
</body>
</html>


        
     

