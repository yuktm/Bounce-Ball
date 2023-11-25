<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bouncing Ball Game</title>
    <style>
        canvas {
            border: 1px solid #000;
            display: block;
            margin: 20px auto;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="600"></canvas>

    <script>
        // Get the canvas element and its context
        var canvas = document.getElementById("gameCanvas");
        var ctx = canvas.getContext("2d");

        // Set initial ball properties
        var ball = {
            x: canvas.width / 2,
            y: canvas.height / 2,
            radius: 20,
            color: "#A3EB17",
            speed: 10,
            dx: 0,
            dy: 0
        };

        // Flag to check if the ball is moving
        var isMoving = false;

        // Function to draw the ball on the canvas
        function drawBall() {
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
            ctx.fillStyle = ball.color;
            ctx.fill();
            ctx.closePath();
        }

        // Function to update the ball's position
        function updateBall() {
            if (isMoving) {
                ball.x += ball.dx;
                ball.y += ball.dy;

                // Bounce off the walls
                if (ball.x + ball.radius > canvas.width || ball.x - ball.radius < 0) {
                    ball.dx = -ball.dx;
                }

                if (ball.y + ball.radius > canvas.height || ball.y - ball.radius < 0) {
                    ball.dy = -ball.dy;
                }
            }
        }

        // Function to clear the canvas
        function clearCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        // Function to update and render the game
        function gameLoop() {
            clearCanvas();
            drawBall();
            updateBall();
            requestAnimationFrame(gameLoop);
        }

        // Event listener to start moving the ball on mouse click
        canvas.addEventListener("click", function(event) {
            isMoving = true;

            // Calculate the direction of the ball based on the click position
            var angle = Math.atan2(event.clientY - ball.y, event.clientX - ball.x);
            ball.dx = ball.speed * Math.cos(angle);
            ball.dy = ball.speed * Math.sin(angle);
        });

        // Start the game loop
        gameLoop();
    </script>
</body>
</html>
