<script>
import { onMount } from 'svelte';
import { fade, fly } from 'svelte/transition';

let canvas;
let ctx;
let showContent = false;

const skills = [
    "Data Analytics",
    "Cyber Security",
    "Machine Learning", 
    "Cloud Security",
    "Neural Networks",
    "Penetration Testing"
];

onMount(() => {
    initMatrix();
    setTimeout(() => showContent = true, 500); 
});

function initMatrix() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    ctx = canvas.getContext('2d');

    const chars = "01";
    const fontSize = 14;
    const columns = canvas.width / fontSize;
    const drops = Array(Math.floor(columns)).fill(1);

    function draw() {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#0F0';
        ctx.font = fontSize + 'px monospace';

        for (let i = 0; i < drops.length; i++) {
            const text = chars[Math.floor(Math.random() * chars.length)];
            ctx.fillText(text, i * fontSize, drops[i] * fontSize);
            if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                drops[i] = 0;
            }
            drops[i]++;
        }
    }

    return setInterval(draw, 33);
}
</script>

<canvas bind:this={canvas} class="matrix-bg"></canvas>
<div class="scanline"></div>
<div class="noise"></div>

{#if showContent}
<main in:fade={{ duration: 1000, delay: 200 }} class="pt-20 md:pt-24">
    <div class="diagonal-split">
        <div class="cyber-container">
            <h1 class="cyber-glitch">ABOUT_</h1>
            
            <div class="content-grid">
                <div class="left-panel" in:fly={{ y: 50, duration: 800 }}>
                    <div class="cyber-terminal">
                        <div class="terminal-header">
                            <div class="controls">
                                <span class="control red"></span>
                                <span class="control yellow"></span>
                                <span class="control green"></span>
                            </div>
                            <span class="title">sys_info.exe</span>
                        </div>
                        <div class="terminal-content">
                            <p>Hello! I'm Jerome Andrew — a curious mind, a builder at heart, and a cybersecurity-aware developer with a passion for transforming complex problems into innovative, real-world solutions.</p>
                            <p>With hands-on experience in data analytics, ethical hacking, and software engineering, I focus on crafting secure, intelligent, and future-ready digital systems that empower organizations to thrive in a connected world.</p>
                        </div>
                    </div>

                    <div class="skill-grid">
                        {#each skills as skill, i}
                            <div class="skill-hex" style="--delay: {i * 0.2}s">
                                <div class="hex-content">{skill}</div>
                            </div>
                        {/each}
                    </div>
                </div>

                <div class="right-panel" in:fly={{ y: 50, duration: 800, delay: 200 }}>
                    <div class="cyber-terminal slant">
                        <div class="terminal-header">
                            <div class="controls">
                                <span class="control red"></span>
                                <span class="control yellow"></span>
                                <span class="control green"></span>
                            </div>
                            <span class="title">mindset.exe</span>
                        </div>
                        <div class="terminal-content">
                            <p>I don't just adapt to emerging technologies — I anticipate and architect them. My strength lies in combining predictive analytics, threat intelligence, and automation to build solutions that don’t just function — they evolve.</p>
                            <p>Every challenge is an opportunity to rethink what's possible — whether it's designing encryption systems, building scalable ML pipelines, or proactively identifying security gaps before they become threats.</p>
                            <p>Outside of code, I’m constantly exploring the intersection of AI, cybersecurity, and data to shape a smarter, safer digital ecosystem — where innovation is secure by design.</p>
                    </div>
                </div>
            </div>

            <div class="cta-section" in:fly={{ y: 50, duration: 800, delay: 400 }}>
                <p class="neon-text">Let’s connect — I’m always looking to collaborate on breakthrough ideas, drive innovation, and build what’s next.</p>
                <a href="https://files.securenotepad.tech/Resume.pdf" class="resume-download glitch-container" target="_blank" rel="noopener noreferrer">
                    <div class="terminal-box">
                        <div class="terminal-header">
                            <div class="controls">
                                <span class="control red"></span>
                                <span class="control yellow"></span>
                                <span class="control green"></span>
                            </div>
                            <span class="title">download_resume.exe</span>
                        </div>
                        <div class="terminal-content">
                            <span class="prompt">[root@system]</span>
                            <span class="command">wget resume.pdf --secure-protocol=TLSv1_2</span>
                            <div class="progress-container">
                                <div class="progress-bar"></div>
                                <div class="progress-text">Initializing secure download...</div>
                            </div>
                        </div>
                    </div>
                </a>
            </div>
        </div>
    </div>
</main>
{/if}

<style>
.matrix-bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    opacity: 0.15;
}

.scanline {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(
        to bottom,
        transparent 50%,
        rgba(0, 255, 0, 0.05) 50%
    );
    background-size: 100% 4px;
    z-index: 1;
    pointer-events: none;
    opacity: 0.1;
}

.noise {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyBAMAAADsEZWCAAAAGFBMVEUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAgE1xQAAAABh0Uk5TACBQcI+fr7/P3+////////////////////9H2B8VAAAAUklEQVQ4y2NgQAX8DKiAH58EAxw0okqw4ZVQRpVgwiehgirBgk+CH1WCG58EF6oEB14JDlQJVnwSbKgSrHglmFElmPFJMKBKMOCT4MSt4wgCALf5V8IF8xWxAAAAAElFTkSuQmCC');
    z-index: 2;
    opacity: 0.03;
    pointer-events: none;
    animation: noise 0.5s steps(2) infinite;
}

.diagonal-split {
    position: relative;
    min-height: 100vh;
    background: linear-gradient(135deg, rgba(0,0,0,0.95) 0%, rgba(0,20,0,0.95) 100%);
    clip-path: polygon(0 0, 100% 0, 100% 95%, 0 100%);
    padding: 1rem 0 4rem;
}

.cyber-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 1rem;
    color: #00ff00;
    overflow-x: hidden;
    padding-bottom: 4rem;
}

@media (min-width: 768px) {
    .cyber-container {
        padding: 2rem;
    }
}

.cyber-glitch {
    font-size: 4rem;
    text-align: center;
    margin-bottom: 3rem;
    color: #00ff00;
    text-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
    position: relative;
    animation: glitch 1s infinite;
}

.content-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1.5rem;
    padding: 0.5rem;
}

@media (min-width: 768px) {
    .content-grid {
        grid-template-columns: 1fr 1fr;
        gap: 2rem;
        padding: 0;
    }
}

.cyber-terminal {
    background: rgba(0, 20, 0, 0.9);
    border: 1px solid #00ff00;
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s ease;
}

.cyber-terminal:hover {
    transform: translateY(-5px);
    box-shadow: 0 0 20px rgba(0, 255, 0, 0.2);
}

.terminal-header {
    background: rgba(0, 40, 0, 0.9);
    padding: 0.5rem 1rem;
    display: flex;
    align-items: center;
    border-bottom: 1px solid #00ff00;
}

.controls {
    display: flex;
    gap: 6px;
    margin-right: 1rem;
}

.control {
    width: 12px;
    height: 12px;
    border-radius: 50%;
}

.red { background: #ff5f56; }
.yellow { background: #ffbd2e; }
.green { background: #27c93f; }

.title {
    color: #00ff00;
    font-family: monospace;
    font-size: 0.9rem;
    opacity: 0.8;
}

.terminal-content {
    padding: 1.5rem;
    color: #00ff00;
    font-family: monospace;
    line-height: 1.6;
}

.terminal-content p {
    margin-bottom: 1rem;
}

.skill-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 0.75rem;
    margin-top: 1.5rem;
    justify-items: center;
}

@media (min-width: 640px) {
    .skill-grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 1rem;
        margin-top: 2rem;
    }
}

.skill-hex {
    width: 100px;
    height: 120px;
    background: rgba(0, 40, 0, 0.9);
    clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #00ff00;
    transition: all 0.3s ease;
    animation: float 3s infinite;
    animation-delay: var(--delay);
}

@media (min-width: 640px) {
    .skill-hex {
        width: 120px;
        height: 140px;
    }
}

.skill-hex:hover {
    transform: scale(1.1);
    box-shadow: 0 0 20px rgba(0, 255, 0, 0.3);
}

.hex-content {
    color: #00ff00;
    text-align: center;
    font-family: monospace;
    padding: 1rem;
}

.slant {
    transform: perspective(1000px) rotateY(-5deg);
}

.cta-section {
    text-align: center;
    margin-top: 4rem;
}

.neon-text {
    color: #00ff00;
    font-size: 1.2rem;
    text-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
    animation: pulse 2s infinite;
}

@keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
}

@keyframes glitch {
    0% { text-shadow: 0 0 10px rgba(0, 255, 0, 0.5); }
    15% { text-shadow: 2px 2px #00ff00, -2px -2px #0ff; }
    30% { text-shadow: -2px -2px #00ff00, 2px 2px #0ff; }
    45% { text-shadow: 0 0 10px rgba(0, 255, 0, 0.5); }
}

@keyframes pulse {
    0%, 100% { text-shadow: 0 0 10px rgba(0, 255, 0, 0.5); }
    50% { text-shadow: 0 0 20px rgba(0, 255, 0, 0.8), 0 0 30px rgba(0, 255, 0, 0.5); }
}

@keyframes noise {
    0%, 100% { transform: translate(0, 0); }
    10% { transform: translate(-5%, -5%); }
    20% { transform: translate(5%, 5%); }
    30% { transform: translate(-5%, 5%); }
    40% { transform: translate(5%, -5%); }
    50% { transform: translate(-5%, -5%); }
    60% { transform: translate(5%, 5%); }
    70% { transform: translate(-5%, 5%); }
    80% { transform: translate(5%, -5%); }
    90% { transform: translate(-5%, -5%); }
}

@media (max-width: 768px) {
    .content-grid {
        grid-template-columns: 1fr;
        gap: 2rem;
        padding: 0.5rem;
    }
    
    .skill-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 1rem;
    }
    
    .cyber-glitch {
        font-size: 2.5rem;
        margin-bottom: 2rem;
    }

    .terminal-content {
        font-size: 0.9rem;
        padding: 1rem;
        word-break: break-word;
    }

    .cyber-terminal {
        margin-bottom: 1.5rem;
    }

    .cta-section {
        margin-top: 2rem;
        padding: 0 1rem;
    }

    .terminal-box {
        margin: 1rem 0;
    }

    .neon-text {
        font-size: 1rem;
        padding: 0 1rem;
    }
}
.resume-download {
    display: block;
    margin: 1.5rem auto;
    width: 100%;
    max-width: min(90vw, 500px);
    text-decoration: none;
    transition: all 0.3s ease;
    position: relative;
}

@media (min-width: 768px) {
    .resume-download {
        margin: 2rem auto;
    }
}
.resume-download:hover {
    transform: translateY(-5px) scale(1.02);
}

.resume-download:hover .terminal-box {
    box-shadow: 0 0 30px rgba(0, 255, 0, 0.4);
    border-color: #00ff00;
}

.resume-download:hover .command {
    color: #fff;
    text-shadow: 0 0 8px rgba(0, 255, 0, 0.8);
}

.resume-download .terminal-box {
    background: rgba(0, 15, 0, 0.95);
    border: 2px solid rgba(0, 255, 0, 0.5);
    border-radius: 10px;
    overflow: hidden;
    transition: all 0.3s ease;
    margin-top: 1.5rem;
}

.resume-download .terminal-content {
    padding: 1rem;
    font-family: 'Courier New', monospace;
    color: #00ff00;
    background: linear-gradient(rgba(0, 20, 0, 0.8), rgba(0, 10, 0, 0.9));
    overflow-x: auto;
    white-space: pre-wrap;
    word-break: break-word;
}

@media (min-width: 768px) {
    .resume-download .terminal-content {
        padding: 1.5rem;
    }
}

.resume-download .prompt {
    color: #00ff00;
    margin-right: 1rem;
    font-weight: bold;
    text-shadow: 0 0 5px rgba(0, 255, 0, 0.5);
}

.resume-download .command {
    color: #00ff00;
    border-right: 2px solid #00ff00;
    padding-right: 1rem;
    animation: blink 1.2s step-end infinite;
    transition: all 0.3s ease;
}

.resume-download .progress-container {
    margin-top: 1rem;
    position: relative;
}

.resume-download .progress-text {
    color: #00ff00;
    font-size: 0.9em;
    margin-top: 0.5rem;
    opacity: 0.8;
    text-align: center;
    animation: pulseText 2s infinite;
}

.progress-bar {
    height: 2px;
    background: #001800;
    margin-top: 0.5rem;
    position: relative;
    overflow: hidden;
}

.progress-bar::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 50%;
    background: #00ff00;
    animation: download 2s ease infinite;
}

@keyframes blink {
    from, to { border-color: transparent; }
    50% { border-color: #00ff00; }
}

@keyframes download {
    0% { transform: translateX(-100%); }
    100% { transform: translateX(200%); }
}

</style>

