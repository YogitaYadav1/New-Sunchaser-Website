<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SunChazer | Ultimate Edition</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@600;800;900&family=Space+Grotesk:wght@700;800&display=swap" rel="stylesheet">
    <style>
        /* --- VARIABLES --- */
        :root {
            --cream: #FFFBF5;
            --cream-dim: #FDEED8;
            --navy: #2D2420;       
            --orange-pop: #FF8800; 
            --gold: #FFD700;       
            --text-main: #443C38;  
            --shadow-deep: 0 25px 50px -12px rgba(255, 136, 0, 0.25);
        }

        /* --- BASE & TYPOGRAPHY --- */
        * { margin: 0; padding: 0; box-sizing: border-box; scroll-behavior: smooth; cursor: none; }
        
        body {
            background-color: var(--cream);
            color: var(--text-main);
            font-family: 'Nunito', sans-serif;
            font-weight: 600;
            overflow-x: hidden;
            line-height: 1.6;
        }

        h1, h2, h3 { 
            font-family: 'Space Grotesk', sans-serif; 
            color: var(--navy); 
            font-weight: 800;
            letter-spacing: -1px;
        }

        /* --- CUSTOM CURSOR --- */
        .cursor-dot {
            width: 12px; height: 12px; background-color: var(--navy);
            position: fixed; top: 0; left: 0; border-radius: 50%;
            z-index: 9999; pointer-events: none;
        }
        .cursor-outline {
            width: 40px; height: 40px; border: 2px solid var(--orange-pop);
            position: fixed; top: 0; left: 0; border-radius: 50%;
            z-index: 9998; pointer-events: none;
            transition: transform 0.15s ease-out;
        }
        .sunbeam-glow {
            position: fixed; top: 0; left: 0; width: 600px; height: 600px;
            background: radial-gradient(circle, rgba(255, 200, 100, 0.15) 0%, transparent 70%);
            transform: translate(-50%, -50%); pointer-events: none; z-index: -1;
        }

        /* --- NAVIGATION --- */
        nav {
            display: flex; justify-content: space-between; align-items: center;
            padding: 25px 5%; position: fixed; width: 100%; top: 0; z-index: 1000;
            background: rgba(255, 251, 245, 0.85); backdrop-filter: blur(15px);
        }
        .logo { font-size: 1.8rem; font-weight: 900; display: flex; align-items: center; gap: 12px; color: var(--navy); }
        .nav-links a {
            margin-left: 35px; text-decoration: none; color: var(--text-main);
            font-weight: 800; font-size: 1.05rem; position: relative;
        }
        .nav-links a::after {
            content: ''; position: absolute; bottom: -6px; left: 0; width: 0; height: 4px;
            background: var(--orange-pop); transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); border-radius: 4px;
        }
        .nav-links a:hover::after { width: 100%; }

        /* --- HERO SECTION --- */
        header {
            min-height: 100vh; display: flex; align-items: center; justify-content: space-between;
            padding: 0 5%; position: relative;
        }
        .hero-content { max-width: 650px; z-index: 2; }
        
        h1 {
            font-size: 5rem; line-height: 1.1; margin-bottom: 25px; min-height: 180px;
            background: linear-gradient(120deg, var(--navy) 0%, var(--orange-pop) 100%);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }

        .typing-cursor {
            display: inline-block; width: 8px; height: 70px;
            background-color: var(--orange-pop);
            animation: blink 1s infinite; margin-left: 10px; vertical-align: middle;
        }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }
        
        .hero-text { font-size: 1.35rem; font-weight: 700; color: #665c57; margin-bottom: 45px; max-width: 90%; }
        
        .btn-primary {
            padding: 18px 42px; background: var(--orange-pop); color: white;
            border-radius: 60px; text-decoration: none; font-weight: 900; font-size: 1.1rem;
            box-shadow: 0 15px 35px rgba(255, 136, 0, 0.4); 
            display: inline-flex; align-items: center; gap: 12px;
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        .btn-primary:hover { transform: scale(1.05) translateY(-5px); box-shadow: 0 20px 40px rgba(255, 136, 0, 0.5); }

        /* --- VISUALS --- */
        .hero-visual { width: 500px; height: 500px; position: relative; perspective: 1000px; display: flex; align-items: center; justify-content: center; }
        .sun-core {
            width: 200px; height: 200px; background: radial-gradient(circle at 30% 30%, var(--gold), var(--orange-pop));
            border-radius: 50%; box-shadow: 0 0 80px rgba(255, 136, 0, 0.6);
            position: absolute; animation: floatSun 6s ease-in-out infinite;
            z-index: 10;
        }
        .orbit-path {
            position: absolute; border: 2px dashed rgba(255, 136, 0, 0.3);
            border-radius: 50%; animation: spin 20s linear infinite;
        }
        .op1 { width: 320px; height: 320px; animation-duration: 12s; }
        .op2 { width: 480px; height: 480px; animation-duration: 20s; animation-direction: reverse; border-width: 1px; }
        
        .rover-planet {
            width: 24px; height: 24px; background: var(--navy); border-radius: 50%;
            position: absolute; top: 50%; left: -12px; transform: translateY(-50%);
            box-shadow: 0 0 20px rgba(45, 36, 32, 0.5);
        }

        @keyframes floatSun { 0%, 100% { transform: translateY(0) scale(1); } 50% { transform: translateY(-20px) scale(1.05); } }
        @keyframes spin { 100% { transform: rotate(360deg); } }

        /* --- SECTIONS --- */
        section { padding: 120px 5%; }
        .section-title { text-align: center; margin-bottom: 80px; font-size: 3rem; font-weight: 900; }
        
        .grid-3d { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 40px; perspective: 1500px; }
        
        .card-3d {
            background: #fff; padding: 50px 35px; border-radius: 35px;
            box-shadow: var(--shadow-deep); transition: transform 0.1s;
            transform-style: preserve-3d; position: relative; overflow: hidden;
            border: 2px solid rgba(255, 255, 255, 0.5);
        }
        .card-3d::before {
            content: ''; position: absolute; top: 0; left: -100%; width: 50%; height: 100%;
            background: linear-gradient(to right, transparent, rgba(255,255,255,0.8), transparent);
            transform: skewX(-25deg); transition: 0.5s; pointer-events: none; z-index: 5;
        }
        .card-3d:hover::before { left: 150%; transition: 0.7s ease-in-out; }

        .card-content { transform: translateZ(30px); text-align: center; }
        .icon-circle {
            width: 80px; height: 80px; border-radius: 50%; background: var(--cream-dim);
            display: inline-flex; align-items: center; justify-content: center;
            font-size: 2rem; color: var(--orange-pop); margin-bottom: 25px;
            box-shadow: inset 0 0 20px rgba(255, 136, 0, 0.1);
        }
        .card-3d h3 { font-size: 1.6rem; margin-bottom: 15px; }
        .card-3d p { font-size: 1.1rem; color: #666; font-weight: 600; }

        /* --- TIMELINE --- */
        .timeline-container { max-width: 850px; margin: 0 auto; position: relative; }
        .timeline-line { position: absolute; left: 40px; top: 0; bottom: 0; width: 6px; background: #E0D0C0; border-radius: 3px; }
        .timeline-progress { position: absolute; left: 40px; top: 0; width: 6px; height: 0%; background: var(--orange-pop); border-radius: 3px; transition: 0.2s; }
        
        .timeline-item { display: flex; margin-bottom: 60px; opacity: 0.2; transform: translateX(50px); transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .timeline-item.active { opacity: 1; transform: translateX(0); }
        
        .time-content { 
            background: #fff; padding: 30px; border-radius: 25px; 
            box-shadow: var(--shadow-deep); flex: 1; margin-left: 40px;
            border-left: 6px solid var(--orange-pop);
        }

        /* --- FOOTER --- */
        footer { text-align: center; padding: 80px 0; font-weight: 700; color: var(--text-main); opacity: 0.8; }

        /* RESPONSIVE */
        @media(max-width: 768px) {
            h1 { font-size: 3.5rem; }
            header { flex-direction: column; text-align: center; justify-content: center; padding-top: 120px; }
            .hero-visual { width: 300px; height: 300px; margin-top: 50px; }
            .sun-core { width: 120px; height: 120px; }
            .nav-links { display: none; }
            .cursor-dot, .cursor-outline, .sunbeam-glow { display: none; }
        }
    </style>
</head>
<body>

    <div class="cursor-dot" id="cursor-dot"></div>
    <div class="cursor-outline" id="cursor-outline"></div>
    <div class="sunbeam-glow" id="sunbeam"></div>

    <nav>
        <div class="logo"><i class="fas fa-sun fa-spin" style="animation-duration:10s; color:var(--orange-pop);"></i> SUNCHAZER</div>
        <div class="nav-links">
            <a href="#home">Overview</a>
            <a href="#features">Specs</a>
            <a href="#logic">Logic</a>
        </div>
        </nav>

    <header id="home">
        <div class="hero-content">
            <h1><span id="typewriter-text"></span><span class="typing-cursor"></span></h1>
            
            <p class="hero-text">A robust ESP8266 rover. It hunts for the sun, optimizes angles, and physically relocates for maximum power.</p>
            <div class="cta-group">
                <a href="#features" class="btn-primary magnetic">Explore Features <i class="fas fa-arrow-down"></i></a>
            </div>
        </div>
        
        <div class="hero-visual">
            <div class="sun-core"></div>
            <div class="orbit-path op1"><div class="rover-planet"></div></div>
            <div class="orbit-path op2"><div class="rover-planet" style="background:var(--orange-pop); box-shadow:0 0 20px var(--orange-pop);"></div></div>
        </div>
    </header>

    <section id="features">
        <h2 class="section-title">ENGINEERED TO PERFORM</h2>
        <div class="grid-3d">
            <div class="card-3d magnetic-card">
                <div class="card-content">
                    <div class="icon-circle"><i class="fas fa-crosshairs"></i></div>
                    <h3>Precision Tracking</h3>
                    <p>Dual-axis servos micro-adjust continuously to lock onto the brightest light source within a 180° hemisphere.</p>
                </div>
            </div>
            <div class="card-3d magnetic-card">
                <div class="card-content">
                    <div class="icon-circle"><i class="fas fa-route"></i></div>
                    <h3>Smart Relocation</h3>
                    <p>Voltage below 3.0V? The rover engages DC motors to physically drive toward the calculated light vector.</p>
                </div>
            </div>
            <div class="card-3d magnetic-card">
                <div class="card-content">
                    <div class="icon-circle"><i class="fas fa-brain"></i></div>
                    <h3>Autonomous Logic</h3>
                    <p>No remote needed. The ESP8266 analyzes sensor data every 3 seconds to make independent movement decisions.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="logic">
        <h2 class="section-title">DECISION LOOP</h2>
        <div class="timeline-container" id="timeline">
            <div class="timeline-line"></div>
            <div class="timeline-progress" id="progressLine"></div>

            <div class="timeline-item">
                <div class="time-content">
                    <h3>01. SCAN ENVIRONMENT</h3>
                    <p>Servos sweep X and Y axes. The system records voltage values at 5-degree increments.</p>
                </div>
            </div>
            <div class="timeline-item">
                <div class="time-content">
                    <h3>02. COMPUTE MAXIMA</h3>
                    <p>The algorithm identifies the coordinates (Angle X, Angle Y) that yielded the highest voltage.</p>
                </div>
            </div>
            <div class="timeline-item">
                <div class="time-content">
                    <h3>03. EXECUTE MOVEMENT</h3>
                    <p>Panels align. If efficiency is still low, the wheels turn to chase the light source.</p>
                </div>
            </div>
        </div>
    </section>

    <footer>
        <p>&copy; 2025 SUNCHAZER PROJECT. BUILT BOLD.</p>
    </footer>

    <script>
        // --- 1. TYPEWRITER ANIMATION LOGIC ---
        const textToType = ["CHASING LIGHT", "AUTOMATICALLY."];
        const typeContainer = document.getElementById('typewriter-text');
        let lineIndex = 0;
        let charIndex = 0;

        function typeWriter() {
            if (lineIndex < textToType.length) {
                const currentLine = textToType[lineIndex];
                
                if (charIndex < currentLine.length) {
                    typeContainer.innerHTML += currentLine.charAt(charIndex);
                    charIndex++;
                    setTimeout(typeWriter, 100); // Speed of typing
                } else {
                    // Line finished
                    if (lineIndex === 0) {
                        typeContainer.innerHTML += "<br>"; // Break line
                        lineIndex++;
                        charIndex = 0;
                        setTimeout(typeWriter, 400); // Pause before next line
                    }
                }
            }
        }
        
        // Start typing on load
        window.onload = typeWriter;

        // --- 2. Custom Cursor & Sunbeam Logic ---
        const cursorDot = document.getElementById('cursor-dot');
        const cursorOutline = document.getElementById('cursor-outline');
        const sunbeam = document.getElementById('sunbeam');

        window.addEventListener('mousemove', (e) => {
            const posX = e.clientX;
            const posY = e.clientY;

            cursorDot.style.transform = `translate(${posX}px, ${posY}px)`;
            sunbeam.style.left = `${posX}px`;
            sunbeam.style.top = `${posY}px`;
            cursorOutline.style.transform = `translate(${posX - 20}px, ${posY - 20}px)`;
        });

        // --- 3. Magnetic Buttons Effect ---
        const magnets = document.querySelectorAll('.magnetic');
        magnets.forEach((magnet) => {
            magnet.addEventListener('mousemove', (e) => {
                const rect = magnet.getBoundingClientRect();
                const x = e.clientX - rect.left - rect.width / 2;
                const y = e.clientY - rect.top - rect.height / 2;
                magnet.style.transform = `translate(${x * 0.3}px, ${y * 0.3}px)`;
            });
            magnet.addEventListener('mouseleave', () => {
                magnet.style.transform = 'translate(0, 0)';
            });
        });

        // --- 4. 3D Card Tilt ---
        const cards = document.querySelectorAll('.magnetic-card');
        cards.forEach(card => {
            card.addEventListener('mousemove', (e) => {
                const rect = card.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;
                const centerX = rect.width / 2;
                const centerY = rect.height / 2;
                const rotateX = ((y - centerY) / 15) * -1;
                const rotateY = (x - centerX) / 15;
                card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.02)`;
            });
            card.addEventListener('mouseleave', () => {
                card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale(1)';
            });
        });

        // --- 5. Timeline Scroll Animation ---
        window.addEventListener('scroll', () => {
            const timeline = document.getElementById('timeline');
            const progressLine = document.getElementById('progressLine');
            const items = document.querySelectorAll('.timeline-item');
            
            const rect = timeline.getBoundingClientRect();
            const start = window.innerHeight * 0.8;
            
            if (rect.top < start) {
                const height = timeline.offsetHeight;
                const scrolled = start - rect.top;
                let percent = (scrolled / height) * 100;
                percent = Math.min(100, Math.max(0, percent));
                progressLine.style.height = `${percent}%`;
            }

            items.forEach(item => {
                const itemTop = item.getBoundingClientRect().top;
                if (itemTop < start) {
                    item.classList.add('active');
                } else {
                    item.classList.remove('active');
                }
            });
        });
    </script>
</body>
</html>
