<script>
import { fly } from 'svelte/transition';
import { onMount } from 'svelte';

let canvas;
let context;
let width;
let height;
let matrix;

const characters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@#$%^&*()*&^%+-/~{[|`]}";
const fontSize = 10;
const columns = [];
let drops = [];

function draw() {
    context.fillStyle = 'rgba(0, 0, 0, 0.05)';
    context.fillRect(0, 0, width, height);
    
    context.fillStyle = '#0F0';
    context.font = fontSize + 'px monospace';
    
    for (let i = 0; i < drops.length; i++) {
        const text = characters.charAt(Math.floor(Math.random() * characters.length));
        context.fillText(text, i * fontSize, drops[i] * fontSize);
        
        if (drops[i] * fontSize > height && Math.random() > 0.975) {
            drops[i] = 0;
        }
        drops[i]++;
    }
}

function initMatrix() {
    width = window.innerWidth;
    height = window.innerHeight;
    canvas.width = width;
    canvas.height = height;
    drops = [];
    for (let i = 0; i < width / fontSize; i++) {
        drops[i] = 1;
    }
}

onMount(() => {
    visible = true;
    context = canvas.getContext('2d');
    initMatrix();
    matrix = setInterval(draw, 35);
    
    const resizeHandler = () => {
        initMatrix();
    };
    
    window.addEventListener('resize', resizeHandler);
    
    return () => {
        clearInterval(matrix);
        window.removeEventListener('resize', resizeHandler);
    };
});

const certificates = [
    {
    title: "Certified Ethical Hacker (CEH v13)",
    link: "https://drive.google.com/file/d/1Tg7jN-2iZs7oYH23CL4p6txL7QfJJcBl/view?usp=sharing",
    organization: "EC-Council",
    date: "June 2025"
    },
    {
    title: "Cyber Security Fundamentals",
    link: "https://www.coursera.org/account/accomplishments/verify/BK5NRV16SRJ0",
    organization: "University of London",
    date: "May 2025"
    },
    {
    title: "AI for Cybersecurity Specialization",
    link: "https://www.coursera.org/account/accomplishments/specialization/U3N82RMLGXH2",
    organization: "The Johns Hopkins University",
    date: "Jan 2025"
    },
    {
    title: "Advanced Malware and Network Anomaly Detection",
    link: "https://www.coursera.org/account/accomplishments/records/EYJIPYPA82H0",
    organization: "The Johns Hopkins University",
    date: "Jan 2025"
    },
    {
    title: "Securing AI and Advanced Topics",
    link: "https://www.coursera.org/account/accomplishments/records/OSUEZA7KCRAM",
    organization: "The Johns Hopkins University",
    date: "Jan 2025"
    },
    {
    title: "Young Turks",
    link: "https://www.naukri.com/campus/certificates/young_turks_round_1_achievement/v0/6707e9bc5abe131f423e1f97",
    organization: "Naukri Campus",
    date: "Oct 2024"
    },
    {
    title: "Data Science",
    link: "https://bit.ly/3Tr8vG2",
    organization: "National Skill Development Corporation",
    date: "Sept 2024"
    },
    {
    title: "Fundamentals of Information Security",
    link: "https://verify.onwingspan.com",
    organization: "Infosys Springboard",
    date: "Aug 2024"
    },
    {
    title: "AIG - Shields Up: Cybersecurity Job Simulation",
    link: "https://forage-uploads-prod.s3.amazonaws.com/completion-certificates/AIG/2ZFnEGEDKTQMtEv9C_AIG_Anqg2EuCSfzvP8Ky9_1715813513638_completion_certificate.pdf",
    organization: "Forage",
    date: "May 2024"
    },
    {
    title: "Cognizant - Artificial Intelligence Job Simulation",
    link: "https://forage-uploads-prod.s3.amazonaws.com/completion-certificates/Cognizant/5N2ygyhzMWjKQmgCK_Cognizant_Anqg2EuCSfzvP8Ky9_1715787563136_completion_certificate.pdf",
    organization: "Forage",
    date: "May 2024"
    },
    {
    title: "Hewlett Packard Enterprise - Software Engineering Job Simulation",
    link: "https://forage-uploads-prod.s3.amazonaws.com/completion-certificates/Hewlett%20Packard%20Enterprise%20/da2T3WZCbMAJD7bNB_Hewlett%20Packard%20Enterprise_Anqg2EuCSfzvP8Ky9_1715809593001_completion_certificate.pdf",
    organization: "Forage",
    date: "May 2024"
    },
    {
    title: "Data Analysis with Python",
    link: "https://coursera.org/verify/XLPD3Z8L4JY7",
    organization: "IBM",
    date: "Feb 2024"
    },
    {
    title: "Developing AI Applications with Python and Flask",
    link: "https://coursera.org/verify/UJS6466EMKG5",
    organization: "IBM",
    date: "Dec 2023"
    },
    {
    title: "Network Defense Essentials NDE",
    link: "https://codered.eccouncil.org/certificate/1d600f04-fd3b-43e4-a9c6-3c3e416fb98b?logged=true",
    organization: "EC-Council",
    date: "July 2023"
    },
    {
    title: "SQL Injection Attacks",
    link: "https://codered.eccouncil.org/certificate/98bff0f6-6b2c-45b0-907b-5f710e194dbf?logged=true",
    organization: "EC-Council",
    date: "Jan 2023"
    },
    {
    title: "Ethical Hacking-Mobile Platforms and Network Architecture",
    link: "https://verify.mygreatlearning.com/verify/DWDSGCAP",
    organization: "Great Learning",
    date: "Dec 2022"
    },
    {
    title: "Game Development Using PyGame",
    link: "https://www.guvi.in/verify-certificate?id=0gq018766R86Y800OW",
    organization: "GUVI Geek Networks, IITM Research Park",
    date: "Dec 2022"
    },
    {
    title: "Python Course on Multiple Languages",
    link: "https://skillsacademy.iitm.ac.in/iitprogram/pages/certificate/9107o657jBd0JYX889.pdf",
    organization: "CODE IIT Madras",
    date: "Dec 2022"
    },
    {
    title: "Diploma in Ethical Hacking",
    link: "https://alison.com/certification/check/%242y%2410%24eeVdQjIzTcaCAEww75V5cOcbggF6KK6GilRi1wZsevYmoufqqv6G",
    organization: "Alison",
    date: "Nov 2022"
    },
    {
    title: "Learn Ethical Hacking From Scratch",
    link: "https://www.udemy.com/certificate/UC-0d62f2e1-81f6-46ab-92e9-d0ae2bd3c6a9/",
    organization: "Udemy",
    date: "Nov 2022"
    }
];

let visible = false;
onMount(() => {
    visible = true;
});
</script>

<canvas bind:this={canvas}></canvas>
<div class="container" class:visible>
<h1 class="glitch" data-text="Certificates">Certificates</h1>

<div class="certificates-grid">
    {#each certificates as cert}
    <div class="certificate-card" 
        transition:fly="{{ y: 20, duration: 300, delay: 300 }}">
        <div class="window-controls">
        <span class="dot red"></span>
        <span class="dot yellow"></span>
        <span class="dot green"></span>
        </div>
        <div class="content">
        <a href={cert.link} target="_blank" rel="noopener noreferrer" class="title">
            <span class="prefix">&gt;</span> {cert.title}
        </a>
        <p class="organization">
            <span class="prefix">$</span> {cert.organization}
        </p>
        <p class="date">
            <span class="prefix">#</span> {cert.date}
        </p>
        </div>
    </div>
    {/each}
</div>
</div>

<style>
canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
}
.container {
    position: relative;
    max-width: 1800px;
    margin: 0 auto;
    padding: 2rem 1rem;
    opacity: 0;
    transition: opacity 0.5s ease-in;
    z-index: 2;
}

.visible {
    opacity: 1;
}

.glitch {
    font-size: 3rem;
    font-weight: bold;
    text-transform: uppercase;
    position: relative;
    text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
                0.025em 0.04em 0 #fffc00;
    animation: glitch 725ms infinite;
    margin-bottom: 2rem;
    color: #fff;
}

.certificates-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
    gap: 1.5rem;
    padding: 0.5rem;
}

.certificate-card {
    background: rgba(0, 0, 0, 0.8);
    border: 1px solid #30fc03;
    border-radius: 8px;
    padding: 1rem;
    transition: all 0.3s ease;
    position: relative;
}

.certificate-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 0 15px rgba(48, 252, 3, 0.5);
}

.window-controls {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
}

.dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
}

.red { background-color: #ff5f56; }
.yellow { background-color: #ffbd2e; }
.green { background-color: #27c93f; }

.content {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.title {
    color: #30fc03;
    text-decoration: none;
    font-size: 1.1rem;
    font-weight: bold;
    line-height: 1.4;
    display: block;
    margin-bottom: 0.5rem;
}

.title:hover {
    text-decoration: underline;
}

.organization, .date {
    color: #b8b8b8;
    margin: 0;
    font-size: 0.9rem;
}

.prefix {
    color: #30fc03;
    margin-right: 0.5rem;
}

@keyframes glitch {
    0% {
    text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
                0.025em 0.04em 0 #fffc00;
    }
    15% {
    text-shadow: 0.05em 0 0 #00fffc, -0.03em -0.04em 0 #fc00ff,
                0.025em 0.04em 0 #fffc00;
    }
    16% {
    text-shadow: -0.05em -0.025em 0 #00fffc, 0.025em 0.035em 0 #fc00ff,
                -0.05em -0.05em 0 #fffc00;
    }
    49% {
    text-shadow: -0.05em -0.025em 0 #00fffc, 0.025em 0.035em 0 #fc00ff,
                -0.05em -0.05em 0 #fffc00;
    }
    50% {
    text-shadow: 0.05em 0.035em 0 #00fffc, 0.03em 0 0 #fc00ff,
                0 -0.04em 0 #fffc00;
    }
    99% {
    text-shadow: 0.05em 0.035em 0 #00fffc, 0.03em 0 0 #fc00ff,
                0 -0.04em 0 #fffc00;
    }
    100% {
    text-shadow: -0.05em 0 0 #00fffc, -0.025em -0.04em 0 #fc00ff,
                -0.04em -0.025em 0 #fffc00;
    }
}
</style>

