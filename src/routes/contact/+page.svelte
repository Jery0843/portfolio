<script>
import { onMount } from 'svelte';
import { fade, fly } from 'svelte/transition';

const contacts = {
    email: [
        { platform: 'Outlook', address: 'jeromeandrewk@outlook.com', icon: '📧' },
        { platform: 'Gmail', address: 'jeromeandrew8888@gmail.com', icon: '📨' }
    ],
    social: [
        { platform: 'Github', url: 'https://github.com/Jery0843', icon: '💻' },
        { platform: 'LinkedIn', url: 'https://www.linkedin.com/in/jeromeandrewk/', icon: '🔗' },
        { platform: 'Instagram', url: 'https://www.instagram.com/jerry_aio/', icon: '📸' }
    ]
};

let canvas;
let ctx;
let showContent = false;
let hoveredLink = null;

const initMatrix = () => {
    const fontSize = 14;
    const columns = Math.floor(window.innerWidth / fontSize);
    const drops = Array(columns).fill(1);
    
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    ctx = canvas.getContext('2d');

    function draw() {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        
        ctx.fillStyle = '#0F0';
        ctx.font = fontSize + 'px monospace';
        
        for (let i = 0; i < drops.length; i++) {
            const text = Math.random() > 0.5 ? '1' : '0';
            ctx.fillText(text, i * fontSize, drops[i] * fontSize);
            
            if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                drops[i] = 0;
            }
            drops[i]++;
        }
    }

    return setInterval(draw, 33);
};

onMount(() => {
    const interval = initMatrix();
    setTimeout(() => showContent = true, 500);
    return () => clearInterval(interval);
});
</script>

<canvas bind:this={canvas} class="matrix-bg"></canvas>
<div class="scanline"></div>

{#if showContent}
<main in:fade={{ duration: 1000, delay: 200 }}>
    <div class="title-section">
        <h1 class="cyber-glitch" data-text="CONTACT">CONTACT</h1>
        <div class="subtitle">$ establish_connection.sh</div>
    </div>

    <div class="terminal-container" in:fly={{ y: 20, duration: 600, delay: 400 }}>
        <div class="terminal-header">
            <div class="controls">
                <div class="dot red"></div>
                <div class="dot yellow"></div>
                <div class="dot green"></div>
            </div>
            <div class="title">contact_protocols.sh</div>
        </div>

        <div class="terminal-content">
            <div class="section">
                <div class="command-line">root@portfolio:~$ cat email_channels.txt</div>
                {#each contacts.email as contact}
                    <div class="contact-item" 
                        on:mouseenter={() => hoveredLink = contact}
                        on:mouseleave={() => hoveredLink = null}>
                        <span class="icon">{contact.icon}</span>
                        <span class="platform">[{contact.platform}]</span>
                        <a href="mailto:{contact.address}" class="link">
                            {contact.address}
                        </a>
                    </div>
                {/each}
            </div>

            <div class="section">
                <div class="command-line">root@portfolio:~$ cat social_networks.txt</div>
                {#each contacts.social as contact}
                    <div class="contact-item"
                        on:mouseenter={() => hoveredLink = contact}
                        on:mouseleave={() => hoveredLink = null}>
                        <span class="icon">{contact.icon}</span>
                        <span class="platform">[{contact.platform}]</span>
                        <a href={contact.url} target="_blank" rel="noopener noreferrer" class="link">
                            {contact.url}
                        </a>
                    </div>
                {/each}
            </div>

            <div class="cursor"></div>
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
        width: 100%;
        height: 100vh;
        position: fixed;
        z-index: 8;
        background: linear-gradient(
            to bottom,
            rgba(255,255,255,0),
            rgba(0,255,0,0.1) 50%,
            rgba(255,255,255,0)
        );
        opacity: 0.1;
        pointer-events: none;
        animation: scanline 6s linear infinite;
    }

    @keyframes scanline {
        0% { transform: translateY(-100%); }
        100% { transform: translateY(100%); }
    }

    main {
        max-width: 1200px;
        margin: 0 auto;
        padding: 2rem;
        color: #00ff00;
        font-family: 'Source Code Pro', monospace;
    }

    .title-section {
        text-align: center;
        margin-bottom: 3rem;
    }

    .cyber-glitch {
        font-size: 4rem;
        position: relative;
        text-transform: uppercase;
        text-shadow: 
            0 0 10px rgba(0,255,0,0.8),
            0 0 20px rgba(0,255,0,0.5),
            0 0 30px rgba(0,255,0,0.3);
        animation: glitch 5s infinite;
    }

    .subtitle {
        color: #00cc00;
        font-size: 1.2rem;
        margin-top: 0.5rem;
    }

    .terminal-container {
        background: rgba(0, 20, 0, 0.95);
        border: 1px solid #00ff00;
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 0 20px rgba(0, 255, 0, 0.2);
    }

    .terminal-header {
        background: #1a1a1a;
        padding: 0.5rem 1rem;
        display: flex;
        align-items: center;
        border-bottom: 1px solid #00ff00;
    }

    .controls {
        display: flex;
        gap: 5px;
        margin-right: 1rem;
    }

    .dot {
        width: 12px;
        height: 12px;
        border-radius: 50%;
    }

    .red { background-color: #ff5f56; }
    .yellow { background-color: #ffbd2e; }
    .green { background-color: #27c93f; }

    .terminal-content {
        padding: 1.5rem;
        position: relative;
    }

    .section {
        margin-bottom: 2rem;
    }

    .command-line {
        color: #00aa00;
        margin-bottom: 1rem;
        font-weight: bold;
    }

    .contact-item {
        display: flex;
        align-items: center;
        gap: 1rem;
        padding: 0.75rem;
        border: 1px solid transparent;
        transition: all 0.3s ease;
    }

    .contact-item:hover {
        background: rgba(0, 255, 0, 0.1);
        border-color: #00ff00;
        transform: translateX(10px);
    }

    .icon {
        font-size: 1.5rem;
    }

    .platform {
        color: #00cc00;
        min-width: 100px;
    }

    .link {
        color: #00ff00;
        text-decoration: none;
        position: relative;
        overflow: hidden;
    }

    .link:hover {
        text-shadow: 0 0 5px #00ff00;
    }

    .link::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 1px;
        background: #00ff00;
        transform: scaleX(0);
        transform-origin: right;
        transition: transform 0.3s ease;
    }

    .link:hover::after {
        transform: scaleX(1);
        transform-origin: left;
    }

    .cursor {
        position: absolute;
        bottom: 1rem;
        left: 1.5rem;
        width: 10px;
        height: 20px;
        background: #00ff00;
        animation: blink 1s step-end infinite;
    }

    @keyframes blink {
        0%, 100% { opacity: 1; }
        50% { opacity: 0; }
    }

    @keyframes glitch {
        0%, 100% { transform: none; opacity: 1; }
        7% { transform: skew(-0.5deg, -0.9deg); opacity: 0.75; }
        10% { transform: none; opacity: 1; }
        27% { transform: none; opacity: 1; }
        30% { transform: skew(0.8deg, -0.1deg); opacity: 0.75; }
        35% { transform: none; opacity: 1; }
        52% { transform: none; opacity: 1; }
        55% { transform: skew(-1deg, 0.2deg); opacity: 0.75; }
        50% { transform: none; opacity: 1; }
        72% { transform: none; opacity: 1; }
        75% { transform: skew(0.4deg, 1deg); opacity: 0.75; }
        80% { transform: none; opacity: 1; }
        100% { transform: none; opacity: 1; }
    }

    @media (max-width: 768px) {
        .cyber-glitch {
            font-size: 2.5rem;
        }

        .contact-item {
            flex-direction: column;
            align-items: flex-start;
            gap: 0.5rem;
        }

        .platform {
            min-width: auto;
        }
    }
</style>

