Test 1
Car Speedometer
Prompt: 
Create a complete HTML file with inline CSS and JavaScript that displays a cinematic car speedometer animation. The speedometer should look like the viewer is racing down a highway, with the needle smoothly accelerating and decelerating in a loop. Use a bold red and black racing theme with glowing neon effects. The design should look modern, high contrast, and dynamic. Center the speedometer on the page, and make sure it has a smooth animated speed needle, glowing tick marks, and an animated background that suggests movement or speed. The final code should be contained in one HTML file, ready to run in a browser.

Tested Models 
Gemini, ChatGPT, Grok,

Grok:




Code:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cinematic Neon Racing Speedometer</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
    background: #000;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Arial', sans-serif;
    perspective: 1000px;
  }


  /* Animated racing road background */
  .background {
    position: absolute;
    top: 0; left: 0; width: 100%; height: 100%;
    background: linear-gradient(to bottom, #001122 0%, #000000 100%);
    overflow: hidden;
    z-index: 1;
  }


  .road {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 100%;
    background: repeating-linear-gradient(
      0deg,
      #111 0px,
      ,
      #111 80px,
      #ff2222 80px,
      #ff2222 100px
    );
    animation: roadMove 0.8s linear infinite;
  }


  @keyframes roadMove {
    0% { transform: translateY(0); }
    100% { transform: translateY(-100px); }
  }


  .speedometer-container {
    position: relative;
    width: 500px;
    height: 500px;
    z-index: 10;
  }


  .speedometer {
    position: relative;
    width: 100%;
    height: 100%;
  }


  /* Outer glow ring */
  .outer-ring {
    position: absolute;
    width: 480px;
    height: 480px;
    top: 10px;
    left: 10px;
    border-radius: 50%;
    background: radial-gradient(circle, transparent 45%, #ff0000 70%, #000 100%);
    box-shadow:
      0 0 60px #ff0000,
      inset 0 0 60px #ff0000;
    animation: pulse 4s infinite alternate;
  }


  @keyframes pulse {
    0% { box-shadow: 0 0 60px #ff0000, inset 0 0 60px #ff0000; }
    100% { box-shadow: 0 0 100px #ff2200, inset 0 0 100px #ff2200; }
  }


  /* Main gauge face */
  .gauge {
    position: absolute;
    width: 420px;
    height: 420px;
    top: 40px;
    left: 40px;
    background: radial-gradient(circle, #111 0%, #000 100%);
    border-radius: 50%;
    box-shadow:
      inset 0 0 80px #000,
      0 0 40px rgba(255,0,0,0.6);
    overflow: hidden;
  }


  /* Neon tick marks */
  .ticks {
    position: absolute;
    width: 100%;
    height: 100%;
  }


  .tick {
    position: absolute;
    width: 4px;
    height: 30px;
    background: linear-gradient(to top, #ff0000, #ff4444);
    left: 50%;
    top: 20px;
    transform-origin: 50% 190px;
    border-radius: 2px;
    box-shadow: 0 0 15px #ff0000;
  }


  .tick.major {
    height: 50px;
    width: 6px;
    box-shadow: 0 0 25px #ff0000;
  }


  /* Speed numbers */
  .number {
    position: absolute;
    color: #ff3333;
    font-size: 28px;
    font-weight: bold;
    text-shadow: 0 0 20px #ff0000;
    transform: translate(-50%, -50%);
  }


  /* Needle */
  .needle-base {
    position: absolute;
    width: 20px;
    height: 20px;
    background: #fff;
    border-radius: 50%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    box-shadow: 0 0 30px #ff0000;
    z-index: 20;
  }


  .needle {
    position: absolute;
    width: 6px;
    height: 240px;
    background: linear-gradient(to top, #ff0000, #ffffff);
    top: 50%;
    left: 50%;
    transform-origin: bottom center;
    border-radius: 3px;
    box-shadow: 0 0 20px #ff0000;
    z-index: 15;
    transition: transform 0.8s cubic-bezier(0.2, 0.8, 0.3, 1);
  }


  /* Digital speed display */
  .digital {
    position: absolute;
    bottom: 80px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 60px;
    font-weight: bold;
    color: #ff0000;
    text-shadow: 0 0 30px #ff0000;
    letter-spacing: 8px;
    z-index: 20;
  }


 20;
  }


  .unit {
    font-size: 24px;
    opacity: 0.8;
  }


  /* Particle speed lines */
  .particles {
    position: absolute;
    width: 100%;
    height: 100%;
    pointer-events: none;
  }


  .particle {
    position: absolute;
    width: 4px;
    height: 60px;
    background: linear-gradient(to bottom, transparent, #ff4444);
    opacity: 0;
    animation: fly 2s linear infinite;
  }


  @keyframes fly {
    0% { opacity: 0; transform: translateY(0) scaleY(0); }
    20% { opacity: 1; }
    100% { opacity: 0; transform: translateY(-800px) scaleY(3); }
  }
</style>
</head>
<body>


<div class="background">
  <div class="road"></div>
</div>


<div class="speedometer-container">
  <div class="outer-ring"></div>
  <div class="gauge">
    <div class="ticks" id="ticks"></div>
    <div class="needle-base"></div>
    <div class="needle" id="needle"></div>
    <div class="digital" id="digital">000 <span class="unit">km/h</span></div>
  </div>
  <div class="particles" id="particles"></div>
</div>


<script>
// Generate tick marks and numbers
const ticksContainer = document.getElementById('ticks');
const totalTicks = 24;
const maxSpeed = 300;


for (let i = 0; i <= totalTicks; i++) {
  const angle = (i / totalTicks) * 270 - 135; // 270° arc from -135° to 135°
  const tick = document.createElement('div');
  tick.className = 'tick' + (i % 3 === 0 ? ' major' : '');
  tick.style.transform = `rotate(${angle}deg)`;
  ticksContainer.appendChild(tick);


  );


  // Add numbers every 3 ticks
  if (i % 3 === 0) {
    const num = document.createElement('div');
    num.className = 'number';
    const speedValue = Math.round((i / totalTicks) * maxSpeed / 10) * 10;
    num.textContent = speedValue;
    const rad = (angle * Math.PI) / 180;
    const radius = 160;
    num.style.left = `50%`;
    num.style.top = `50%`;
    num.style.transform = `translate(calc(-50% + ${Math.cos(rad) * radius}px), calc(-50% + ${Math.sin(rad) * radius}px)) rotate(${angle + 135}deg)`;
    ticksContainer.appendChild(num);
  }
}


// Needle animation loop
const needle = document.getElementById('needle');
const digital = document.getElementById('digital');
let currentSpeed = 0;
let targetSpeed = 0;
let accelerating = true;


function updateSpeed() {
  // Smooth acceleration / deceleration cycle
  if (accelerating) {
    targetSpeed += 2;
    if (targetSpeed >= 280) accelerating = false;
  } else {
    targetSpeed -= 1.5;
    if (targetSpeed <= 0) accelerating = true;
  }


  // Smooth needle movement
  currentSpeed += (targetSpeed - currentSpeed) * 0.08;
  const angle = (currentSpeed / maxSpeed) * 270 - 135;
  needle.style.transform = `translateX(-50%) rotate(${angle}deg)`;


  // Update digital display
  digital.innerHTML = Math.round(currentSpeed).toString().padStart(3, '0') + ' <span class="unit">km/h</span>';
 
  requestAnimationFrame(updateSpeed);
}


updateSpeed();


// Add speed particles
const particlesContainer = document.getElementById('particles');
setInterval(() => {
  if (currentSpeed > 100) {
    for (let i = 0; i < 3; i++) {
      const p = document.createElement('div');
      p.className = 'particle';
      p.style.left = Math.random() * 100 + '%';
      p.style.animationDelay = Math.random() * 0.5 + 's';
      p.style.animationDuration = (1 + Math.random()) + 's';
      particlesContainer.appendChild(p);
      setTimeout(() => p.remove(), 3000);
    }
  }
}, 200);
</script>


</body>
</html>

Gemini:


Code:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cinematic Racing Speedometer</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Load Inter font */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
       
        :root {
            --primary-red: #ff003c;
            --secondary-black: #1a1a1a;
            --dark-background: #0d0d0d;
            --neon-glow: 0 0 5px var(--primary-red), 0 0 10px var(--primary-red), 0 0 20px rgba(255, 0, 60, 0.7);
            --needle-color: #f7e034;
            --needle-shadow: 0 0 10px #f7e034;
        }


        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--dark-background);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow: hidden; /* Prevent scroll from background animation */
        }


        /* Cinematic Background Effect (Simulates motion) */
        .cinematic-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 200%; /* Wider than viewport for parallax/motion effect */
            height: 100%;
            /* Diagonal dark lines for speed/road effect */
            background-image: repeating-linear-gradient(
                -45deg,
                var(--secondary-black) 0,
                var(--secondary-black) 2px,
                var(--dark-background) 2px,
                var(--dark-background) 40px
            );
            animation: moveBackground 15s linear infinite;
            z-index: -1;
            opacity: 0.3;
        }


        @keyframes moveBackground {
            from { transform: translateX(0); }
            to { transform: translateX(-50%); }
        }


        .speedometer-container {
            position: relative;
            width: 400px;
            height: 400px;
            border-radius: 50%;
            background: radial-gradient(circle at center, #2e2e2e 0%, var(--secondary-black) 60%, var(--dark-background) 100%);
            box-shadow: 0 0 50px rgba(0, 0, 0, 0.5), inset 0 0 20px rgba(255, 255, 255, 0.05);
            border: 5px solid var(--primary-red);
            padding: 20px;
            overflow: hidden;
        }


        .speedometer-dial {
            position: relative;
            width: 100%;
            height: 100%;
            border-radius: 50%;
        }


        /* Needle Styling */
        .needle {
            position: absolute;
            bottom: 50%;
            left: 50%;
            width: 50%;
            height: 5px;
            transform-origin: 0% 50%;
            /* Initial rotation for 0 MPH (135 degrees offset from vertical) */
            transform: rotate(135deg);
            background-color: var(--needle-color);
            box-shadow: var(--needle-shadow);
            z-index: 10;
            transition: transform 0.1s linear; /* Smooth movement */
        }


        .needle::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -10px;
            width: 10px;
            height: 9px;
            background: var(--needle-color);
            border-radius: 50%;
            box-shadow: var(--needle-shadow);
        }


        .center-pin {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: var(--primary-red);
            border: 4px solid var(--needle-color);
            box-shadow: var(--neon-glow), 0 0 15px var(--needle-color);
            z-index: 15;
        }


        /* Tick Marks and Labels */
        .tick-container {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
        }


        /* Function to generate dynamic tick marks (implemented in JS for complexity)
           Here is the base style for a tick */
        .tick {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 2px;
            height: 100%;
            transform-origin: 0 0;
        }


        .tick span {
            position: absolute;
            display: block;
            background: var(--primary-red);
            box-shadow: var(--neon-glow);
            width: 2px;
            height: 10px;
            top: -190px;
            left: -1px;
            border-radius: 1px;
        }


        .tick-label {
            position: absolute;
            color: #ffffff;
            font-size: 14px;
            font-weight: 600;
            text-shadow: var(--neon-glow);
        }


        /* Digital Speed Display */
        .speed-display {
            position: absolute;
            bottom: 10%;
            left: 50%;
            transform: translateX(-50%);
            text-align: center;
            color: var(--primary-red);
            z-index: 20;
            padding: 10px 20px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            border: 1px solid var(--primary-red);
            box-shadow: var(--neon-glow);
        }


        #current-speed {
            font-size: 4rem;
            line-height: 1;
            font-weight: 900;
            color: var(--needle-color);
            text-shadow: var(--needle-shadow), var(--neon-glow);
        }


        .units {
            font-size: 1rem;
            color: var(--primary-red);
            font-weight: 600;
        }


    </style>
</head>
<body class="bg-gray-900">


    <div class="cinematic-background"></div>


    <div class="speedometer-container rounded-full">
        <h1 class="text-white text-xl font-bold text-center pt-4" style="text-shadow: var(--neon-glow);">NITRO BOOST</h1>
        <div class="speedometer-dial">
           
            <!-- Dynamic Ticks and Labels will be inserted here by JavaScript -->
            <div class="tick-container" id="tick-container"></div>
           
            <div class="needle" id="speed-needle"></div>
            <div class="center-pin"></div>


            <div class="speed-display">
                <div id="current-speed">000</div>
                <div class="units">MPH</div>
            </div>
        </div>
    </div>


    <script>
        // --- Speedometer Constants ---
        const MIN_SPEED = 0;
        const MAX_SPEED = 240;
        const START_ANGLE = 135; // 0 MPH starting angle
        const END_ANGLE = 45;    // 240 MPH ending angle (clockwise)
        const ARC_ANGLE = 360 - (START_ANGLE - END_ANGLE); // 270 degrees arc
        const CENTER_X = 200; // Half of container width (400px)
        const CENTER_Y = 200; // Half of container height (400px)
        const RADIUS = 160;


        // --- DOM Elements ---
        const needle = document.getElementById('speed-needle');
        const speedDisplay = document.getElementById('current-speed');
        const tickContainer = document.getElementById('tick-container');


        // --- Animation State ---
        let currentTime = 0;
        let lastTime = 0;
        let targetSpeed = 0;
        let currentSpeed = 0;
        const maxAcceleration = 80; // Max speed change per second
        const maxDeceleration = 60;


        /**
         * Maps a speed value to the corresponding rotation angle for the needle.
         * The angle goes from 135deg (0 MPH) to 405deg (240 MPH).
         * @param {number} speed - The current speed value.
         * @returns {number} The rotation angle in degrees.
         */
        function speedToAngle(speed) {
            const ratio = (speed - MIN_SPEED) / (MAX_SPEED - MIN_SPEED);
            // Angle range is 135deg to 405deg (135 + 270)
            return START_ANGLE + (ratio * ARC_ANGLE);
        }


        /**
         * Generates the speedometer tick marks and labels.
         */
        function generateTicks() {
            const majorTicks = 13; // 0, 20, 40, ..., 240
            const step = (MAX_SPEED - MIN_SPEED) / (majorTicks - 1);
           
            for (let i = 0; i < majorTicks; i++) {
                const speedValue = i * step;
                const angle = speedToAngle(speedValue);


                // 1. Create the Tick Mark (Red Glow)
                const tickEl = document.createElement('div');
                tickEl.className = 'tick';
                tickEl.style.transform = `translate(-50%, -50%) rotate(${angle}deg)`;
               
                const span = document.createElement('span');
                // Give special styling to the maximum speed tick
                if (speedValue === MAX_SPEED) {
                    span.style.boxShadow = '0 0 10px #00ffc8, 0 0 20px #00ffc8, 0 0 30px #00ffc8';
                    span.style.backgroundColor = '#00ffc8';
                    span.style.height = '15px';
                }
                tickEl.appendChild(span);
                tickContainer.appendChild(tickEl);


                // 2. Create the Label (Speed Number)
                const labelEl = document.createElement('div');
                labelEl.className = 'tick-label';
                labelEl.textContent = speedValue;
               
                // Calculate position for the label (slightly outside the tick)
                const labelAngleRad = (angle - 90) * (Math.PI / 180); // Adjust for CSS 0deg top
                const labelX = CENTER_X + RADIUS * Math.cos(labelAngleRad);
                const labelY = CENTER_Y + RADIUS * Math.sin(labelAngleRad);


                // Center the label text around the calculated point
                labelEl.style.left = `${labelX}px`;
                labelEl.style.top = `${labelY}px`;
                labelEl.style.transform = 'translate(-50%, -50%)';


                // Give special styling to the maximum speed label
                 if (speedValue === MAX_SPEED) {
                    labelEl.style.color = '#00ffc8';
                    labelEl.style.textShadow = '0 0 5px #00ffc8, 0 0 10px #00ffc8';
                }
               
                tickContainer.appendChild(labelEl);
            }
        }


        /**
         * Randomly determines a new target speed for the needle to move towards.
         */
        function setNewTargetSpeed() {
            // Target speed bounces between high and low ranges for a cinematic effect
            const isHighSpeed = Math.random() > 0.5;
            if (isHighSpeed) {
                targetSpeed = Math.floor(Math.random() * (MAX_SPEED - 180) + 180); // High speed burst
            } else {
                targetSpeed = Math.floor(Math.random() * (100 - 50) + 50); // Cruising speed
            }
            // Ensure target is within min/max bounds
            targetSpeed = Math.max(MIN_SPEED, Math.min(MAX_SPEED, targetSpeed));
        }




        /**
         * Main animation loop. Updates the speed and needle position smoothly.
         * @param {number} timestamp - The current time in milliseconds.
         */
        function animateSpeedometer(timestamp) {
            if (lastTime === 0) {
                lastTime = timestamp;
            }
            const deltaTime = (timestamp - lastTime) / 1000; // Delta time in seconds
            lastTime = timestamp;


            // Check if we need a new target
            if (Math.abs(currentSpeed - targetSpeed) < 1) {
                setNewTargetSpeed();
            }


            // Determine speed change based on acceleration/deceleration limits
            let speedDelta = targetSpeed - currentSpeed;
            let maxChange = 0;


            if (speedDelta > 0) {
                // Accelerating
                maxChange = maxAcceleration * deltaTime;
            } else {
                // Decelerating (or braking)
                maxChange = maxDeceleration * deltaTime;
            }


            // Apply change, capping it at the max allowed change for smoothness
            if (Math.abs(speedDelta) > maxChange) {
                speedDelta = speedDelta > 0 ? maxChange : -maxChange;
            }
           
            // Update the speed
            currentSpeed += speedDelta;
           
            // Clamp speed to boundaries
            currentSpeed = Math.max(MIN_SPEED, Math.min(MAX_SPEED, currentSpeed));


            // 1. Update Needle Rotation
            const newAngle = speedToAngle(currentSpeed);
            needle.style.transform = `rotate(${newAngle}deg)`;


            // 2. Update Digital Display (Always show 3 digits)
            const roundedSpeed = Math.round(currentSpeed);
            speedDisplay.textContent = roundedSpeed.toString().padStart(3, '0');


            requestAnimationFrame(animateSpeedometer);
        }


        // --- Initialization ---
        window.onload = function() {
            generateTicks();
            setNewTargetSpeed(); // Start with an initial target speed
            animateSpeedometer(0); // Start the main animation loop
        };


    </script>
</body>
</html>

ChatGPT:


Code:
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cinematic Speedometer</title>
<style>
    html, body {
        margin: 0;
        height: 100%;
        background: #000;
        overflow: hidden;
        font-family: Arial, sans-serif;
    }


    /* Animated moving background */
    body::before {
        content: "";
        position: fixed;
        top: 0;
        left: 0;
        width: 200%;
        height: 200%;
        background: radial-gradient(circle at center, #222 0%, #000 70%) fixed,
                    repeating-linear-gradient(
                        90deg,
                        rgba(255,0,0,0.15) 0px,
                        rgba(255,0,0,0.15) 4px,
                        rgba(0,0,0,0) 4px,
                        rgba(0,0,0,0) 12px
                    );
        animation: bgmove 5s linear infinite;
        filter: blur(2px);
        z-index: -1;
    }


    @keyframes bgmove {
        0% { transform: translateX(0); }
        100% { transform: translateX(-200px); }
    }


    /* Center speedometer container */
    .container {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }


    canvas {
        display: block;
        width: 500px;
        height: 500px;
    }
</style>
</head>
<body>


<div class="container">
    <canvas id="speedometer" width="500" height="500"></canvas>
</div>


<script>
const canvas = document.getElementById("speedometer");
const ctx = canvas.getContext("2d");


const centerX = canvas.width / 2;
const centerY = canvas.height / 2;
const radius = 200;


let speed = 0;
let increasing = true;


// Draw glowing text
function glowText(text, x, y, size, color) {
    ctx.font = size + "px Arial";
    ctx.fillStyle = color;
    ctx.shadowBlur = 20;
    ctx.shadowColor = color;
    ctx.fillText(text, x, y);
    ctx.shadowBlur = 0;
}


// Draw speedometer
function drawSpeedometer() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);


    // Outer glow ring
    ctx.beginPath();
    ctx.arc(centerX, centerY, radius + 20, 0, Math.PI * 2);
    ctx.strokeStyle = "rgba(255,0,0,0.4)";
    ctx.lineWidth = 10;
    ctx.shadowBlur = 30;
    ctx.shadowColor = "red";
    ctx.stroke();
    ctx.shadowBlur = 0;


    // Tick marks
    for (let i = 0; i <= 180; i += 6) {
        const angle = (Math.PI * (i - 90)) / 180;
        const inner = radius - 15;
        const outer = radius;
        const x1 = centerX + inner * Math.cos(angle);
        const y1 = centerY + inner * Math.sin(angle);
        const x2 = centerX + outer * Math.cos(angle);
        const y2 = centerY + outer * Math.sin(angle);


        ctx.beginPath();
        ctx.moveTo(x1, y1);
        ctx.lineTo(x2, y2);


        ctx.strokeStyle = "rgba(255,40,40," + (i % 30 === 0 ? "1" : "0.3") + ")";
        ctx.lineWidth = i % 30 === 0 ? 4 : 2;


        ctx.shadowBlur = i % 30 === 0 ? 20 : 10;
        ctx.shadowColor = "red";
        ctx.stroke();
        ctx.shadowBlur = 0;
    }


    // Needle
    const needleAngle = (speed - 90) * (Math.PI / 180);
    const needleLength = radius - 40;


    ctx.beginPath();
    ctx.moveTo(centerX, centerY);
    ctx.lineTo(
        centerX + needleLength * Math.cos(needleAngle),
        centerY + needleLength * Math.sin(needleAngle)
    );
    ctx.strokeStyle = "red";
    ctx.lineWidth = 6;
    ctx.shadowBlur = 25;
    ctx.shadowColor = "red";
    ctx.stroke();
    ctx.shadowBlur = 0;


    // Center circle
    ctx.beginPath();
    ctx.arc(centerX, centerY, 12, 0, Math.PI * 2);
    ctx.fillStyle = "black";
    ctx.shadowBlur = 20;
    ctx.shadowColor = "red";
    ctx.fill();
    ctx.shadowBlur = 0;


    // Speed text
    glowText(Math.floor((speed / 180) * 240) + " km/h", centerX - 70, centerY + 80, 32, "red");
}


// Animate needle acceleration and deceleration
function animate() {
    if (increasing) {
        speed += 0.7;
        if (speed >= 180) increasing = false;
    } else {
        speed -= 0.7;
        if (speed <= 0) increasing = true;
    }


    drawSpeedometer();
    requestAnimationFrame(animate);
}


drawSpeedometer();
animate();
</script>


</body>
</html>


