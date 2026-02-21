# 2-month
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2 Months | Our Growth</title>
    <style>
        :root {
            --primary: #ff4d6d;
            --bg: #0a0a0a;
            --text: #ffffff;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow-x: hidden;
        }

        #canvas-bg {
            position: fixed;
            top: 0;
            left: 0;
            z-index: 1;
        }

        .container {
            position: relative;
            z-index: 2;
            background: rgba(15, 15, 15, 0.95);
            padding: 30px;
            border: 1px solid var(--primary);
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(255, 77, 109, 0.3);
            max-width: 500px;
            width: 85%;
            text-align: center;
        }

        .terminal-header {
            border-bottom: 1px solid #333;
            margin-bottom: 20px;
            padding-bottom: 10px;
            font-size: 0.7rem;
            color: var(--primary);
            display: flex;
            justify-content: space-between;
            letter-spacing: 2px;
        }

        #text-box {
            font-size: 1rem;
            line-height: 1.6;
            text-align: left;
            min-height: 180px;
            margin-bottom: 20px;
        }

        #unlock-btn {
            background: transparent;
            border: 1px solid var(--primary);
            color: var(--primary);
            padding: 12px 24px;
            cursor: pointer;
            transition: all 0.4s;
            font-family: 'Courier New', Courier, monospace;
            font-weight: bold;
            display: none;
            margin: 0 auto;
        }

        #unlock-btn:hover {
            background: var(--primary);
            color: white;
            box-shadow: 0 0 20px var(--primary);
        }

        #tree-container {
            margin-top: 20px;
            display: none;
        }

        svg {
            width: 100%;
            height: 300px;
        }

        .heart-bloom {
            fill: var(--primary);
            opacity: 0;
            animation: bloom 2s forwards;
        }

        @keyframes bloom {
            to { opacity: 1; transform: scale(1.2); }
        }

        .cursor {
            display: inline-block;
            width: 10px;
            height: 18px;
            background: var(--primary);
            animation: blink 0.8s infinite;
        }

        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }
    </style>
</head>
<body>

<canvas id="canvas-bg"></canvas>

<div class="container">
    <div class="terminal-header">
        <span>STRENGTH_OS v2.0</span>
        <span>UPTIME: 60_DAYS</span>
    </div>
    
    <div id="text-box"></div>
    <span class="cursor" id="cursor"></span>

    <button id="unlock-btn" onclick="startGrowth()">[ INITIALIZE_GROWTH_PROTOCOL ]</button>

    <div id="tree-container">
        <svg id="tree-svg" viewBox="0 0 400 400"></svg>
        <p style="color: var(--primary); font-size: 0.9rem; margin-top: 15px;">
            "Our love isn't perfect, but it's alive. Happy 2 months."
        </p>
    </div>
</div>

<script>
    const lines = [
        "> Initializing emotional scan...",
        "> Arguments detected: 60/60 days.",
        "> Resilience levels: Off the charts.",
        "> Result: You are doing better than you think.",
        "> I don't want easy. I want YOU.",
        "> My sunshine. My life.",
        "> Click below to see what we're building..."
    ];

    let l = 0, c = 0;
    const box = document.getElementById('text-box');
    const btn = document.getElementById('unlock-btn');

    function typeWriter() {
        if (l < lines.length) {
            if (c < lines[l].length) {
                box.innerHTML += lines[l].charAt(c);
                c++;
                setTimeout(typeWriter, 35);
            } else {
                box.innerHTML += "<br>";
                l++; c = 0;
                setTimeout(typeWriter, 600);
            }
        } else {
            document.getElementById('cursor').style.display = 'none';
            btn.style.display = 'block';
        }
    }

    // Tree Logic
    const svg = document.getElementById('tree-svg');
    function drawBranch(x1, y1, angle, depth) {
        if (depth === 0) {
            // Bloom a heart at the end of the branch
            const heart = document.createElementNS("http://www.w3.org/2000/svg", "text");
            heart.setAttribute("x", x1 - 5);
            heart.setAttribute("y", y1);
            heart.setAttribute("class", "heart-bloom");
            heart.setAttribute("style", `animation-delay: ${Math.random() * 2}s`);
            heart.textContent = "❤️";
            heart.style.fontSize = "12px";
            svg.appendChild(heart);
            return;
        }

        const x2 = x1 + Math.cos(angle * Math.PI / 180) * depth * 8;
        const y2 = y1 + Math.sin(angle * Math.PI / 180) * depth * 8;

        const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
        line.setAttribute("x1", x1); line.setAttribute("y1", y1);
        line.setAttribute("x2", x2); line.setAttribute("y2", y2);
        line.setAttribute("stroke", "#5c3d2e");
        line.setAttribute("stroke-width", depth);
        svg.appendChild(line);

        setTimeout(() => {
            drawBranch(x2, y2, angle - 25, depth - 1);
            drawBranch(x2, y2, angle + 25, depth - 1);
        }, 100);
    }

    function startGrowth() {
        btn.style.display = 'none';
        document.getElementById('tree-container').style.display = 'block';
        drawBranch(200, 380, -90, 8);
    }

    // Matrix Background
    const canvas = document.getElementById('canvas-bg');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    const hearts = Array(20).fill(0).map(() => ({ x: Math.random()*canvas.width, y: Math.random()*canvas.height, s: Math.random()*2+1 }));
    function animate() {
        ctx.fillStyle = "rgba(10, 10, 10, 0.1)";
        ctx.fillRect(0,0,canvas.width, canvas.height);
        ctx.fillStyle = "#ff4d6d";
        hearts.forEach(h => {
            ctx.fillText("❤️", h.x, h.y);
            h.y += h.s;
            if(h.y > canvas.height) h.y = -10;
        });
        requestAnimationFrame(animate);
    }
    animate();
    setTimeout(typeWriter, 1000);
</script>

</body>
</html>
