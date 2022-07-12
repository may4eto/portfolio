<script>
    export let data 
</script>

<div class="card">
    <h2>Experiences</h2>
   {#each data.experiences as experience} 
        <div class="experience">
            <img src="images/{experience.image}" alt="" />
            <div>
                <span>{experience.dates}</span>
                <h3>{experience.role}</h3>
                <p>{experience.description}</p>
            </div>
        </div>
   {/each}
</div>

<style>
    .card h3 {
        font-size: 16px;
        margin: 8px 0;
        font-weight: 600;
    }
    .card p {
        font-size: 16px;
        color: var(--text-color-grey);
    }
    .card .experience {
        display: flex;
    }
    .card .experience:not(:last-child) {
        margin-bottom: 32px;
    }
    .card .experience img {
        max-width: 100px;
        height: auto;
        object-fit: contain;
        margin-right: 24px;
    }
    .card .experience span {
        display: block;
        font-size: 14px;
        color: var(--text-color-grey);
    }
    @media (max-width: 540px) {
        .card .experience {
            flex-direction: column;
            align-items: center;
            margin-bottom: 24px;
        }
        .card .experience img {
            margin: 0 0 16px 0;
        }
        .card .experience span, .card .experience h3 {
            text-align: center;
        }
    }
</style>