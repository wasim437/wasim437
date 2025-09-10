<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Snake Animation</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: #fff;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            position: relative;
        }

        .container {
            max-width: 900px;
            width: 100%;
            padding: 20px;
            z-index: 10;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            background: linear-gradient(to right, #12c2e9, #c471ed, #f64f59);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        }

        .subtitle {
            font-size: 1.2rem;
            opacity: 0.8;
            margin-bottom: 20px;
        }

        .snake-container {
            position: relative;
            width: 100%;
            height: 400px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }

        button {
            background: linear-gradient(to right, #12c2e9, #c471ed);
            border: none;
            padding: 12px 25px;
            border-radius: 30px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        .instructions {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 10px;
            margin-top: 30px;
            backdrop-filter: blur(5px);
        }

        .instructions h2 {
            margin-bottom: 15px;
            color: #12c2e9;
        }

        .instructions ol {
            padding-left: 20px;
            line-height: 1.6;
        }

        .instructions li {
            margin-bottom: 10px;
        }

        .particle {
            position: absolute;
            background: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            pointer-events: none;
        }

        .github-link {
            position: absolute;
            bottom: 20px;
            right: 20px;
            color: rgba(255, 255, 255, 0.7);
            text-decoration: none;
            font-size: 0.9rem;
            transition: color 0.3s ease;
        }

        .github-link:hover {
            color: white;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2rem;
            }
            
            .snake-container {
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>GitHub Snake Animation</h1>
            <p class="subtitle">A beautiful, interactive snake animation for your GitHub profile</p>
        </header>
        
        <div class="snake-container">
            <canvas id="snakeCanvas"></canvas>
        </div>
        
        <div class="controls">
            <button id="speedUp">Speed Up</button>
            <button id="slowDown">Slow Down</button>
            <button id="changeColor">Change Colors</button>
        </div>
        
        <div class="instructions">
            <h2>How to add to your GitHub README</h2>
            <ol>
                <li>Copy the HTML code from this file</li>
                <li>Create a new repository with the name your_username.github.io</li>
                <li>Add an index.html file with the copied code</li>
                <li>In your profile README, add: <code>[![Snake Animation](https://your_username.github.io)](https://your_username.github.io)</code></li>
            </ol>
        </div>
    </div>
    
    <a href="https://github.com" class="github-link">View on GitHub</a>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const canvas = document.getElementById('snakeCanvas');
            const ctx = canvas.getContext('2d');
            
            // Set canvas size
            canvas.width = canvas.offsetWidth;
            canvas.height = canvas.offsetHeight;
            
            // Snake properties
            let snake = [];
            let food = {};
            let gridSize = 20;
            let direction = 'right';
            let nextDirection = 'right';
            let gameSpeed = 150;
            let score = 0;
            let cellSize;
            let colors = {
                snakeHead: '#12c2e9',
                snakeBody: '#c471ed',
                food: '#f64f59',
                background: 'rgba(0, 0, 0, 0.2)'
            };
            
            // Initialize game
            function initGame() {
                // Calculate cell size based on canvas and grid size
                cellSize = Math.min(canvas.width, canvas.height) / gridSize;
                
                // Initialize snake
                snake = [
                    {x: 5, y: Math.floor(gridSize / 2)},
                    {x: 4, y: Math.floor(gridSize / 2)},
                    {x: 3, y: Math.floor(gridSize / 2)}
                ];
                
                // Generate first food
                generateFood();
                
                // Start game loop
                gameLoop();
            }
            
            // Generate food at random position
            function generateFood() {
                food = {
                    x: Math.floor(Math.random() * gridSize),
                    y: Math.floor(Math.random() * gridSize)
                };
                
                // Make sure food doesn't appear on snake
                for (let i = 0; i < snake.length; i++) {
                    if (snake[i].x === food.x && snake[i].y === food.y) {
                        generateFood();
                        break;
                    }
                }
            }
            
            // Main game loop
            function gameLoop() {
                update();
                draw();
                setTimeout(gameLoop, gameSpeed);
            }
            
            // Update game state
            function update() {
                // Update direction
                direction = nextDirection;
                
                // Calculate new head position
                let newHead = {x: snake[0].x, y: snake[0].y};
                
                switch(direction) {
                    case 'up': newHead.y--; break;
                    case 'down': newHead.y++; break;
                    case 'left': newHead.x--; break;
                    case 'right': newHead.x++; break;
                }
                
                // Wrap around edges
                if (newHead.x < 0) newHead.x = gridSize - 1;
                if (newHead.x >= gridSize) newHead.x = 0;
                if (newHead.y < 0) newHead.y = gridSize - 1;
                if (newHead.y >= gridSize) newHead.y = 0;
                
                // Check for collision with self
                for (let i = 0; i < snake.length; i++) {
                    if (snake[i].x === newHead.x && snake[i].y === newHead.y) {
                        // Reset game
                        initGame();
                        return;
                    }
                }
                
                // Add new head
                snake.unshift(newHead);
                
                // Check for food collision
                if (newHead.x === food.x && newHead.y === food.y) {
                    score++;
                    generateFood();
                    createParticles(newHead.x * cellSize + cellSize/2, newHead.y * cellSize + cellSize/2);
                } else {
                    // Remove tail
                    snake.pop();
                }
            }
            
            // Draw everything
            function draw() {
                // Clear canvas
                ctx.fillStyle = colors.background;
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                
                // Draw snake
                for (let i = 0; i < snake.length; i++) {
                    // Draw rounded segments
                    ctx.beginPath();
                    
                    if (i === 0) {
                        ctx.fillStyle = colors.snakeHead;
                    } else {
                        // Gradient for body
                        let gradient = ctx.createLinearGradient(
                            snake[i].x * cellSize, 
                            snake[i].y * cellSize,
                            snake[i].x * cellSize + cellSize,
                            snake[i].y * cellSize + cellSize
                        );
                        gradient.addColorStop(0, colors.snakeHead);
                        gradient.addColorStop(1, colors.snakeBody);
                        ctx.fillStyle = gradient;
                    }
                    
                    ctx.roundRect(
                        snake[i].x * cellSize + 2, 
                        snake[i].y * cellSize + 2, 
                        cellSize - 4, 
                        cellSize - 4,
                        8
                    );
                    ctx.fill();
                    
                    // Add eyes to head
                    if (i === 0) {
                        ctx.fillStyle = 'white';
                        
                        // Position eyes based on direction
                        let eyeSize = cellSize / 6;
                        let offset = cellSize / 3;
                        
                        if (direction === 'right') {
                            ctx.beginPath();
                            ctx.arc(snake[i].x * cellSize + cellSize - offset, snake[i].y * cellSize + offset, eyeSize, 0, Math.PI * 2);
                            ctx.arc(snake[i].x * cellSize + cellSize - offset, snake[i].y * cellSize + cellSize - offset, eyeSize, 0, Math.PI * 2);
                            ctx.fill();
                        } else if (direction === 'left') {
                            ctx.beginPath();
                            ctx.arc(snake[i].x * cellSize + offset, snake[i].y * cellSize + offset, eyeSize, 0, Math.PI * 2);
                            ctx.arc(snake[i].x * cellSize + offset, snake[i].y * cellSize + cellSize - offset, eyeSize, 0, Math.PI * 2);
                            ctx.fill();
                        } else if (direction === 'up') {
                            ctx.beginPath();
                            ctx.arc(snake[i].x * cellSize + offset, snake[i].y * cellSize + offset, eyeSize, 0, Math.PI * 2);
                            ctx.arc(snake[i].x * cellSize + cellSize - offset, snake[i].y * cellSize + offset, eyeSize, 0, Math.PI * 2);
                            ctx.fill();
                        } else if (direction === 'down') {
                            ctx.beginPath();
                            ctx.arc(snake[i].x * cellSize + offset, snake[i].y * cellSize + cellSize - offset, eyeSize, 0, Math.PI * 2);
                            ctx.arc(snake[i].x * cellSize + cellSize - offset, snake[i].y * cellSize + cellSize - offset, eyeSize, 0, Math.PI * 2);
                            ctx.fill();
                        }
                    }
                }
                
                // Draw food with pulsing effect
                let pulse = Math.sin(Date.now() / 200) * 0.2 + 0.8;
                ctx.fillStyle = colors.food;
                ctx.beginPath();
                ctx.arc(
                    food.x * cellSize + cellSize/2,
                    food.y * cellSize + cellSize/2,
                    cellSize/2 * pulse,
                    0,
                    Math.PI * 2
                );
                ctx.fill();
                
                // Draw score
                ctx.fillStyle = 'white';
                ctx.font = '20px Arial';
                ctx.textAlign = 'right';
                ctx.fillText(`Score: ${score}`, canvas.width - 20, 30);
            }
            
            // Handle keyboard input
            document.addEventListener('keydown', function(e) {
                switch(e.key) {
                    case 'ArrowUp':
                        if (direction !== 'down') nextDirection = 'up';
                        break;
                    case 'ArrowDown':
                        if (direction !== 'up') nextDirection = 'down';
                        break;
                    case 'ArrowLeft':
                        if (direction !== 'right') nextDirection = 'left';
                        break;
                    case 'ArrowRight':
                        if (direction !== 'left') nextDirection = 'right';
                        break;
                }
            });
            
            // Create particles for effects
            function createParticles(x, y) {
                for (let i = 0; i < 15; i++) {
                    let particle = document.createElement('div');
                    particle.className = 'particle';
                    document.body.appendChild(particle);
                    
                    // Random size and color
                    let size = Math.random() * 5 + 2;
                    let colorIndex = Math.floor(Math.random() * 3);
                    let colors = ['#12c2e9', '#c471ed', '#f64f59'];
                    
                    particle.style.width = `${size}px`;
                    particle.style.height = `${size}px`;
                    particle.style.backgroundColor = colors[colorIndex];
                    particle.style.boxShadow = `0 0 ${size*2}px ${colors[colorIndex]}`;
                    
                    // Set initial position
                    particle.style.left = `${x}px`;
                    particle.style.top = `${y}px`;
                    
                    // Random movement
                    let angle = Math.random() * Math.PI * 2;
                    let speed = Math.random() * 3 + 2;
                    let dx = Math.cos(angle) * speed;
                    let dy = Math.sin(angle) * speed;
                    
                    // Animate particle
                    let opacity = 1;
                    let particleInterval = setInterval(() => {
                        x += dx;
                        y += dy;
                        opacity -= 0.03;
                        
                        particle.style.left = `${x}px`;
                        particle.style.top = `${y}px`;
                        particle.style.opacity = opacity;
                        
                        if (opacity <= 0) {
                            clearInterval(particleInterval);
                            particle.remove();
                        }
                    }, 30);
                }
            }
            
            // Control buttons
            document.getElementById('speedUp').addEventListener('click', function() {
                gameSpeed = Math.max(50, gameSpeed - 20);
            });
            
            document.getElementById('slowDown').addEventListener('click', function() {
                gameSpeed = Math.min(300, gameSpeed + 20);
            });
            
            document.getElementById('changeColor').addEventListener('click', function() {
                // Generate random colors
                colors.snakeHead = getRandomColor();
                colors.snakeBody = getRandomColor();
                colors.food = getRandomColor();
            });
            
            // Generate random bright color
            function getRandomColor() {
                let letters = '0123456789ABCDEF';
                let color = '#';
                for (let i = 0; i < 6; i++) {
                    color += letters[Math.floor(Math.random() * 16)];
                }
                return color;
            }
            
            // Handle window resize
            window.addEventListener('resize', function() {
                canvas.width = canvas.offsetWidth;
                canvas.height = canvas.offsetHeight;
                cellSize = Math.min(canvas.width, canvas.height) / gridSize;
            });
            
            // Initialize the game
            initGame();
        });
    </script>
</body>
</html>
