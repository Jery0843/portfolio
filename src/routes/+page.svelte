<script lang="ts">
import HackerTerminal from '$lib/components/HackerTerminal.svelte';
import { onMount } from 'svelte';

const introLines = [
    '> Initializing secure connection...',
    '> System check: OK',
    '> ACCESS_GRANTED: root@jerome:~$',
    '> Hey there, I\'m Jerome!',
    '> Welcome to my digital playground',
];

let canvas;
let ctx;

onMount(() => {
    initMatrix();
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

    setInterval(draw, 33);
}
</script>

<canvas bind:this={canvas} class="matrix-bg"></canvas>
<div class="scanline"></div>
<div class="crt"></div>

<div class="container mx-auto px-4 py-8 min-h-screen flex items-start justify-center bg-transparent pt-16">
    <div class="flex flex-col md:flex-row items-center justify-between w-full max-w-7xl gap-8">
        <div class="w-full md:w-1/2 p-4 md:p-8">
            <div class="terminal-glow">
                <div class="terminal-header">
                    <div class="terminal-buttons">
                        <span class="terminal-button red"></span>
                        <span class="terminal-button yellow"></span>
                        <span class="terminal-button green"></span>
                    </div>
                    <div class="terminal-title">jerome@system:~$</div>
                </div>
                <div class="terminal-inner">
                    <HackerTerminal lines={introLines} typingSpeed={35} />
                </div>
            </div>
        </div>
        <div class="w-full md:w-1/2 flex justify-center p-4 md:p-6">
            <div class="profile-container w-full max-w-[300px] md:max-w-[400px]">
                <div class="glitch">
                    <div class="glitch__base">
                        <img 
                            src="https://securehive.securenotepad.tech/Snapchat-1649986276~2.jpg" 
                            alt="Jerome's Profile"
                        />
                    </div>
                    <div class="glitch__layer">
                        <img 
                            src="https://securehive.securenotepad.tech/Snapchat-1649986276~2.jpg" 
                            alt="Jerome's Profile"
                        />
                    </div>
                    <div class="glitch__layer">
                        <img 
                            src="https://securehive.securenotepad.tech/Snapchat-1649986276~2.jpg" 
                            alt="Jerome's Profile"
                        />
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

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
    background: repeating-linear-gradient(
        0deg,
        rgba(0, 255, 0, 0) 0%,
        rgba(0, 255, 0, 0.05) 0.5%,
        rgba(0, 255, 0, 0) 1%
    );
    background-size: 100% 4px;
    animation: scanline 10s linear infinite;
    pointer-events: none;
    z-index: 2;
}

.crt {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
    pointer-events: none;
    background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%);
    background-size: 100% 4px;
}
.terminal-glow {
    background: rgba(0, 0, 0, 0.9);
    padding: 1rem;
    min-height: 200px;
    min-width: min(400px, 90vw);
    max-width: 500px;
    border: 1px solid rgba(0, 255, 0, 0.4);
    box-shadow: 0 0 10px rgba(0, 255, 0, 0.3),
            0 0 20px rgba(0, 255, 0, 0.2),
            0 0 30px rgba(0, 255, 0, 0.1),
            inset 0 0 20px rgba(0, 255, 0, 0.2);
    position: relative;
    overflow: hidden;
    animation: terminalPulse 4s infinite;
}

.terminal-inner {
    min-height: 250px;
    padding: 1.5rem;
    background: rgba(0, 0, 0, 0.6);
    border-radius: 8px;
    position: relative;
    z-index: 2;
}

.profile-container {
    position: relative;
    aspect-ratio: 4/5;
    border-radius: 20px;
    overflow: hidden;
    background: linear-gradient(45deg, rgba(0, 255, 0, 0.3), rgba(0, 255, 0, 0.1));
    padding: 3px;
}

.glitch {
    position: relative;
    width: 100%;
    height: 100%;
    border-radius: 18px;
    overflow: hidden;
    animation: glitchShift 8s infinite;
    opacity: 0.5;
    mix-blend-mode: screen;
}

.glitch__base {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    animation: glitch-vertical 2s infinite linear alternate-reverse;
    opacity: 0.4;
    filter: contrast(1.5) brightness(0.8);
}

.glitch__layer {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    animation: glitch-layers 3s infinite alternate-reverse;
    opacity: 0.4;
    mix-blend-mode: exclusion;
    filter: saturate(200%) contrast(150%);
}

.glitch__layer:nth-child(2) {
    animation-delay: -2s;
    animation-duration: 3s;
    filter: hue-rotate(90deg);
}

.glitch__layer:nth-child(3) {
    animation-delay: -1s;
    animation-duration: 3.5s;
    filter: hue-rotate(180deg);
}

.glitch__main img,
.glitch__base img,
.glitch__layer img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    border-radius: 18px;
}

.glitch__color {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    mix-blend-mode: multiply;
    animation: glitch-anim-color 4s infinite linear alternate;
}

.glitch__color img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 18px;
}

.glitch__color--red {
    animation-delay: 0.5s;
    filter: hue-rotate(0deg);
}

.glitch__color--green {
    animation-delay: 1s;
    filter: hue-rotate(120deg);
}

.glitch__color--blue {
    animation-delay: 1.5s;
    filter: hue-rotate(240deg);
}

@keyframes glitch-anim-color {
    0% {
        transform: translate(0);
        opacity: 0.1;
    }
    2% {
        transform: translate(-8px, 5px);
        opacity: 0.3;
    }
    4% {
        transform: translate(8px, -5px);
        opacity: 0.3;
    }
    6% {
        transform: translate(-8px, 5px);
        opacity: 0.3;
    }
    8% {
        transform: translate(0);
        opacity: 0.1;
    }
    100% {
        transform: translate(0);
        opacity: 0.1;
    }
}

@keyframes terminalPulse {
    0%, 100% { box-shadow: 0 0 10px rgba(0, 255, 0, 0.3),
                        0 0 20px rgba(0, 255, 0, 0.2),
                        0 0 30px rgba(0, 255, 0, 0.1),
                        inset 0 0 20px rgba(0, 255, 0, 0.2); }
    50% { box-shadow: 0 0 20px rgba(0, 255, 0, 0.4),
                    0 0 40px rgba(0, 255, 0, 0.3),
                    0 0 60px rgba(0, 255, 0, 0.2),
                    inset 0 0 40px rgba(0, 255, 0, 0.3); }
}

@keyframes glitchShift {
    0%, 100% { transform: translate(0); filter: hue-rotate(0deg); }
    25% { transform: translate(-10px, 5px); filter: hue-rotate(90deg); }
    50% { transform: translate(5px, -5px); filter: hue-rotate(180deg); }
    75% { transform: translate(-5px, 10px); filter: hue-rotate(270deg); }
}

.scanline {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(to bottom,
        rgba(255,255,255,0),
        rgba(0,255,0,0.1) 50%,
        rgba(0,255,0,0));
    animation: scanline 6s linear infinite;
    pointer-events: none;
    z-index: 10;
}

@keyframes scanline {
    0% { transform: translateY(-100%); }
    100% { transform: translateY(100%); }
}
</style>
