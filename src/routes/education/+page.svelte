<script>
import { onMount } from 'svelte';
let visible = false;

onMount(() => {
    visible = true;
});
</script>

<div class="education-container" class:visible>
    <h1 class="glowing-text">> Education_History</h1>

    <div class="timeline">
        <!-- CEH Entry -->
        <div class="timeline-entry left">
            <div class="content-box">
                <div class="terminal-header">
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <h3 class="typewriter">REDTEAM HACKER ACADEMY, CHENNAI</h3>
                </div>
                <div class="terminal-content">
                    <p class="duration">2024 - Present</p>
                    <p class="degree">CEH (Certified Ethical Hacker)</p>
                    
                </div>
            </div>
        </div>
        
        <!-- MSc Entry -->
        <div class="timeline-entry right">
            <div class="content-box">
                <div class="terminal-header">
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <h3 class="typewriter">LOYOLA COLLEGE, CHENNAI</h3>
                </div>
                <div class="terminal-content">
                    <p class="duration">2022 - 2024</p>
                    <p class="degree">M.Sc in Computer Science</p>
                    <p class="grade">CGPA : 8.5</p>
                </div>
            </div>
        </div>

        <!-- BSc Entry -->
        <div class="timeline-entry left">
            <div class="content-box">
                <div class="terminal-header">
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <h3 class="typewriter">LOYOLA COLLEGE OF ARTS AND SCIENCE</h3>
                </div>
                <div class="terminal-content">
                    <p class="duration">2019 - 2022</p>
                    <p class="degree">B.Sc in Computer Science</p>
                    <p class="grade">GRADE : A+</p>
                </div>
            </div>
        </div>

        <!-- High School Entry -->
        <div class="timeline-entry right">
            <div class="content-box">
                <div class="terminal-header">
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <span class="circles"></span>
                    <h3 class="typewriter">JOHN BRITTO MATRIC HR. SEC. SCHOOL</h3>
                </div>
                <div class="terminal-content">
                    <p class="duration">2017 - 2019</p>
                    <p class="degree">Higher Secondary Education</p>
                </div>
            </div>
        </div>
    </div>
</div>

<style>
:global(body) {
    background: #000;
}

.education-container {
    padding: 3rem;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.5s ease-out;
}

.education-container.visible {
    opacity: 1;
    transform: translateY(0);
}

.glowing-text {
    color: #00ff00;
    text-shadow: 0 0 5px #00ff00, 0 0 15px #00ff00, 0 0 25px #00ff00;
    font-family: 'Courier New', monospace;
    margin-bottom: 3rem;
    font-size: 2.2rem;
}

.timeline {
    position: relative;
    max-width: 1200px;
    margin: 0 auto;
}

.timeline::after {
    content: '';
    position: absolute;
    width: 2px;
    background: #00ff00;
    top: 0;
    bottom: 0;
    left: 50%;
    box-shadow: 0 0 10px #00ff00;
}

.timeline-entry {
    position: relative;
    width: 50%;
    padding: 1.5rem;
    margin-bottom: 3rem;
}

.right {
    left: 50%;
}

.left {
    left: 0;
}

.content-box {
    background: rgba(0, 0, 0, 0.8);
    border: 2px solid #00ff00;
    border-radius: 8px;
    box-shadow: 0 0 15px #00ff00;
    overflow: hidden;
    transition: all 0.3s ease;
}

.content-box:hover {
    transform: scale(1.03);
    box-shadow: 0 0 30px #00ff00;
}

.terminal-header {
    background: #1a1a1a;
    padding: 0.5rem;
    border-bottom: 1px solid #00ff00;
    display: flex;
    align-items: center;
}

.circles {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #ff5f56;
    margin-right: 6px;
    display: inline-block;
}

.circles:nth-child(2) {
    background: #ffbd2e;
}

.circles:nth-child(3) {
    background: #27c93f;
}

.terminal-content {
    padding: 1.5rem;
    font-size: 1.1rem;
}

.typewriter {
    color: #00ff00;
    font-family: 'Courier New', monospace;
    margin: 0 0 0 1rem;
    font-size: 1.3rem;
}

.duration {
    color: #00ff00;
    font-family: 'Courier New', monospace;
    margin-bottom: 0.5rem;
}

.degree {
    color: #fff;
    font-family: 'Courier New', monospace;
    margin-bottom: 0.5rem;
}

.grade {
    color: #00ff00;
    font-family: 'Courier New', monospace;
}

@media (max-width: 768px) {
    .timeline::after {
        left: 31px;
    }

    .timeline-entry {
        width: 100%;
        padding-left: 70px;
        padding-right: 25px;
    }

    .right {
        left: 0;
    }
}
</style>

