<script>
    export let data
</script>

<div class="card">
    <h2>Skills</h2>
    {#each data.skills as skill}
        <div class="skill">  
            <span>{skill.name}</span>
            <div class="bar">
                <div class="fill" style="width: {skill.mastery}"></div>
            </div>
        </div>
    {/each}
</div>

<style>
    .card .skill {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .card .skill .bar {
        height: 12px;
        width: 66%;
        background-color: var(--light-grey);
        border-radius: 12px;
    }
    .card .skill .bar .fill {
        background-color: var(--text-color-grey);
        height: 100%;
        border-radius: 12px;
    }
    @media(min-width: 1024px) and (max-width: 1278px) {
        .card .skill:last-child {
            margin-bottom: 20px;
        }
    }
   
</style>