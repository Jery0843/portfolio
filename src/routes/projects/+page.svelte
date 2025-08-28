<script>
import { onMount } from 'svelte';
import { fade } from 'svelte/transition';

let canvas;
let context;
let selectedProject = null;
let showContent = false;

const projects = [
    {
    title: "HackTheBox & TryHackMe Labs",
    url: "https://htb-writeups.securenotepad.tech/",
    duration: "Ongoing",
    affiliation: "Self-Study",
    overview: "Hands-on penetration testing practice through HackTheBox and TryHackMe platforms, covering real-world attack scenarios and advanced exploitation techniques.",
    focusAreas: {
        "Web Application Security": [
        "SQL Injection, XSS, CSRF, and authentication bypasses"
        ],
        "Privilege Escalation": [
        "Windows and Linux privilege escalation via misconfigurations and kernel exploits"
        ],
        "Network Exploitation": [
        "Enumeration and exploitation of services using Nmap, Hydra, and Metasploit"
        ],
        "Reverse Engineering & Forensics": [
        "Analyzed binaries, memory dumps, and applied reverse engineering techniques"
        ]
    },
    stack: {
        Tools: "Burp Suite, Metasploit, Nmap, John the Ripper, Hydra",
        Skills: "Privilege Escalation, Web Exploitation, Reverse Engineering, Forensics"
    },
    significance: "Strengthened offensive security skills in a controlled environment by solving real-world inspired challenges, ranking among top performers in selected labs."
},
    {
    title: "CloudSEK CTF",
    url: "https://medium.com/@OxJerry/cloudsek-ctf-report-aug-2025-e494f880001a",
    duration: "Aug 2025",
    affiliation: "CloudSEK",
    overview: "Participated in CloudSEK’s Capture the Flag (CTF) challenge, simulating real-world penetration testing scenarios with a focus on web applications, authentication mechanisms, and API exploitation.",
    highlights: {
        "Reconnaissance & OSINT": [
        "Gathered intelligence from leaked GitHub commits and public assets"
        ],
        "AI Prompt Injection": [
        "Exploited weak system prompt controls in an AI chatbot to retrieve sensitive data"
        ],
        "GraphQL Exploitation": [
        "Performed schema introspection and JWT forgery with alg:none to escalate privileges"
        ],
        "Authentication Attacks": [
        "Bypassed Multi-Factor Authentication via insecure backup code API"
        ],
        "Advanced SSRF": [
        "Investigated server-side request forgery vectors to probe internal metadata services"
        ]
    },
    stack: {
        Tools: "Nmap, Burp Suite, Wireshark, Python",
        Techniques: "OSINT, AI Prompt Injection, GraphQL Exploitation, JWT Forgery, MFA Bypass, SSRF"
    },
    significance: "Demonstrated advanced penetration testing skills by chaining vulnerabilities to achieve privileged access, while also providing remediation strategies."
},
    {
    title: "SecureHive",
    url: "https://securehive.securenotepad.tech/",
    duration: "May 2024 - Dec 2024",
    affiliation: "Red Team Hacker Academy",
    overview: "SecureHive is a sophisticated Python-based file and folder encryption application designed to provide robust data security through advanced cryptographic techniques.",
    features: {
        "Advanced Encryption": [
        "Implemented AES for file encryption",
        "Utilized RSA for secure key management"
        ],
        "Hash Integrity Verification": [
        "SHA-256 hash generation for encrypted files",
        "Integrity checks to detect unauthorized modifications"
        ],
        "Master Password Protection": [
        "Strong password enforcement",
        "Limited incorrect login attempts",
        "Email notifications for security alerts"
        ],
        "Security Monitoring": [
        "Automated email alerts for suspicious activities",
        "Comprehensive security tracking"
        ]
    },
    stack: {
        Languages: "Python",
        Frameworks: "PyQt6",
        "Encryption Algorithms": "AES, RSA",
        "Hash Algorithm": "SHA-256",
        "Security Features": "Master password, email notifications, progress tracking, integrity verification"
    },
    significance: "Demonstrates advanced cybersecurity skills by creating a user-friendly application with enterprise-grade encryption and integrity verification capabilities, bridging technical complexity with intuitive design."
    },
    {
    title: "Predicting Patient No-Show with Data Analysis",
    url: "https://ijnrd.org/viewpaperforall.php?paper=IJNRD2403501",
    duration: "Dec 2023 - Mar 2024",
    affiliation: "KANINI",
    overview: "Developed a predictive machine learning model to forecast patient no-shows, aiming to optimize healthcare scheduling and improve care delivery.",
    methodologies: {
        "Data Preparation": [
        "Cleaned and preprocessed appointment data",
        "Integrated demographics, health information, and historical no-show data"
        ],
        "Feature Engineering": [
        "Appointment lead time",
        "Patient historical patterns",
        "Demographic insights"
        ],
        "Model Development": [
        "Logistic Regression",
        "Random Forest Classifier"
        ],
        "Model Evaluation": [
        "Accuracy",
        "Precision",
        "Recall",
        "Area Under ROC Curve (AUC)"
        ]
    },
    stack: {
        Technologies: "Python, Machine Learning",
        Libraries: "Scikit-learn, Pandas, NumPy",
        Visualization: "Matplotlib, Seaborn"
    },
    impact: "Created a strategic tool enabling healthcare providers to reduce no-show rates, enhance operational efficiency, and improve patient care management."
    },
    {
    title: "Kali Secure Notepad",
    url: "https://securenotepad.tech/",
    duration: "Jun 2023 - Nov 2023",
    affiliation: "Loyola College",
    overview: "Developed an advanced, privacy-focused note-taking application designed to provide secure data storage with robust encryption and user-friendly interface.",
    features: {
        "Advanced Encryption": [
        "Strong encryption algorithms",
        "Comprehensive password protection"
        ],
        "Security Monitoring": [
        "Email notifications for incorrect password attempts",
        "Hash integrity checks to prevent unauthorized modifications"
        ],
        "Platform": [
        "Leveraged Kali Linux cybersecurity capabilities"
        ]
    },
    stack: {
        Languages: "Python",
        "Security Techniques": [
        "Encryption algorithms",
        "Authentication mechanisms",
        "Integrity verification"
        ]
    },
    significance: "Created a secure note-taking solution that balances high-level data privacy, intuitive user experience, and advanced cybersecurity techniques."
    }
];

onMount(() => {
    initMatrix();
    setTimeout(() => showContent = true, 500);
});

function initMatrix() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    context = canvas.getContext('2d');

    const fontSize = 14;
    const columns = Math.floor(canvas.width / fontSize);
    const drops = Array(columns).fill(1);
    const chars = "01";

    function draw() {
    context.fillStyle = 'rgba(0, 0, 0, 0.05)';
    context.fillRect(0, 0, canvas.width, canvas.height);
    
    context.fillStyle = '#0F0';
    context.font = `${fontSize}px monospace`;
    
    for (let i = 0; i < drops.length; i++) {
        const text = chars[Math.floor(Math.random() * chars.length)];
        context.fillText(text, i * fontSize, drops[i] * fontSize);
        
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

{#if showContent}
<main in:fade={{ duration: 1000, delay: 200 }}>
    <div class="title-section">
    <div class="cyber-container">
        <div class="circuit-pattern"></div>
        <h1 class="cyber-glitch">PROJECTS</h1>
    </div>
    <div class="subtitle">> Exploring the depths of cybersecurity</div>
    </div>

    <div class="projects-grid">
    {#each projects as project}
        <div 
        class="project-card" 
        class:expanded={selectedProject === project}
        on:click={() => selectedProject = selectedProject === project ? null : project}
        >
        <div class="card-header">
            <div class="controls">
            <div class="dot red"></div>
            <div class="dot yellow"></div>
            <div class="dot green"></div>
            </div>
            <a 
            href={project.url} 
            class="project-title" 
            target="_blank" 
            on:click|stopPropagation
            >
            > {project.title}
            </a>
        </div>

        <div class="meta-info">
            <p class="duration">$ Duration: {project.duration}</p>
            <p class="affiliation"># Affiliation: {project.affiliation}</p>
        </div>

        <div class="content">
            <div class="section">
            <h3>> Overview</h3>
            <p>{project.overview}</p>
            </div>

            {#if project.features}
            <div class="section">
                <h3>> Features</h3>
                {#each Object.entries(project.features) as [category, items]}
                <div class="category">
                    <h4>{category}:</h4>
                    <ul>
                    {#each items as item}
                        <li>{item}</li>
                    {/each}
                    </ul>
                </div>
                {/each}
            </div>
            {/if}

            {#if project.methodologies}
            <div class="section">
                <h3>> Methodologies</h3>
                {#each Object.entries(project.methodologies) as [category, items]}
                <div class="category">
                    <h4>{category}:</h4>
                    <ul>
                    {#each items as item}
                        <li>{item}</li>
                    {/each}
                    </ul>
                </div>
                {/each}
            </div>
            {/if}

            <div class="section">
            <h3>> Technical Stack</h3>
            {#each Object.entries(project.stack) as [category, items]}
                <div class="stack-item">
                <h4>{category}:</h4>
                {#if Array.isArray(items)}
                    <ul>
                    {#each items as item}
                        <li>{item}</li>
                    {/each}
                    </ul>
                {:else}
                    <p>{items}</p>
                {/if}
                </div>
            {/each}
            </div>

            {#if project.significance}
            <div class="section">
                <h3>> Significance</h3>
                <p>{project.significance}</p>
            </div>
            {/if}

            {#if project.impact}
            <div class="section">
                <h3>> Impact</h3>
                <p>{project.impact}</p>
            </div>
            {/if}
        </div>
        </div>
    {/each}
    </div>
</main>
{/if}

<style>
:global(body) {
    background-color: #000;
    color: #0F0;
    margin: 0;
    font-family: 'Source Code Pro', monospace;
}

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
    height: 2px;
    background: rgba(0, 255, 0, 0.1);
    opacity: 0.75;
    animation: scanning 3s linear infinite;
    z-index: 999;
    pointer-events: none;
}

@keyframes scanning {
    0% { transform: translateY(0); }
    100% { transform: translateY(100vh); }
}

main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
}

.title-section {
    text-align: center;
    margin-bottom: 4rem;
}

.cyber-container {
    position: relative;
    display: inline-block;
}

.cyber-glitch {
    font-size: 3.5rem;
    text-transform: uppercase;
    animation: glitch 1s infinite;
    text-shadow: 
    0 0 5px #0F0,
    0 0 10px #0F0,
    0 0 15px #0F0;
}

@keyframes glitch {
    0% { text-shadow: 2px 0 0 red, -2px 0 0 blue; }
    41.99% { text-shadow: 2px 0 0 red, -2px 0 0 blue; }
    42% { text-shadow: none; }
    43% { text-shadow: none; }
    43.01% { text-shadow: 2px 0 0 red, -2px 0 0 blue; }
    100% { text-shadow: 2px 0 0 red, -2px 0 0 blue; }
}

.subtitle {
    color: #0F0;
    font-size: 1.2rem;
    margin-top: 1rem;
}

.projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
}

.project-card {
    background: rgba(0, 20, 0, 0.95);
    border: 1px solid #0F0;
    border-radius: 8px;
    padding: 1.5rem;
    transition: all 0.3s ease;
    cursor: pointer;
    position: relative;
    overflow: hidden;
}

.project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 0 20px rgba(0, 255, 0, 0.2);
}

.project-card.expanded {
    grid-column: 1 / -1;
    cursor: default;
}

.card-header {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
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

.red { background: #ff5f56; }
.yellow { background: #ffbd2e; }
.green { background: #27c93f; }

.project-title {
    color: #0F0;
    text-decoration: none;
    font-size: 1.2rem;
    font-weight: bold;
}

.project-title:hover {
    text-decoration: underline;
}

.meta-info {
    font-size: 0.9rem;
    opacity: 0.8;
    margin-bottom: 1rem;
}

.content {
    opacity: 0.9;
}

.section {
    margin-bottom: 1.5rem;
}

h3 {
    color: #0F0;
    border-bottom: 1px solid #0F0;
    padding-bottom: 0.5rem;
    margin-bottom: 1rem;
}

h4 {
    color: #0F0;
    margin: 0.5rem 0;
}

ul {
    list-style-type: none;
    padding-left: 1.5rem;
}

li::before {
    content: ">";
    color: #0F0;
    margin-right: 0.5rem;
}

@media (max-width: 768px) {
    .projects-grid {
    grid-template-columns: 1fr;
    }
    
    .cyber-glitch {
    font-size: 2.5rem;
    }
}
</style>

