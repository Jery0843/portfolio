<script>
const experiences = [
    {
    company: "Kanini Software Solutions | Chennai",
    position: "Data & Analytics Intern",
    duration: "Dec 2023 – Apr 2024",
    achievements: [
        "Performed exploratory data analysis (EDA) on large datasets to derive insights and improve healthcare scheduling by 20%.",
        "Built and optimized machine learning models for predicting patient no-shows, increasing prediction accuracy by 15%."
    ]
    },
    {
    company: "Mic & Mac Solutions | Chennai",
    position: "Web Development Intern",
    duration: "May 2023 – Jun 2023",
    achievements: [
        "Developed full-stack web applications using ASP.NET and CSS, improving application response times by 30%.",
        "Used SQL to manage and optimize databases, improving query performance by 25%."
    ]
    }
];
</script>

<div class="experience-timeline">
<h1 class="text-3xl font-bold text-hacker-green mb-12 terminal-glow">Professional Experience</h1>
{#each experiences as exp}
    <div class="experience-item">
    <h2 class="company-name">{exp.company}</h2>
    <h3 class="position">{exp.position}</h3>
    <p class="duration">{exp.duration}</p>
    <ul class="achievements">
        {#each exp.achievements as achievement}
        <li>{achievement}</li>
        {/each}
    </ul>
    </div>
{/each}
</div>
