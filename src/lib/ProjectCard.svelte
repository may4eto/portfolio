<script>
    export let project = {}
</script>

<div class="card">
    <img src="images/{project.image}" alt=""  />
    <div class="tags">
            {#each project.tags as tag}
            <span>
                #{tag} 
            </span>
            {/each}
    </div>
    <h3>{project.name}</h3>
    <p>{@html project.description}</p>
    <div class="links">
        <a href="{project.url}" target="_blank">Demo</a>
        <a href="{project.repo}" target="_blank">Code</a>
    </div>
</div>

<style>
    .card span {
        font-size: 16px;
        margin-right: 8px;
    }
    .card h3 {
        margin: 0 0 8px 0;
    }
    .card img {
        width: 100%;
        height: 140px;
        border-radius: 8px;
    }
    .card p {
        font-size: 16px;
        color: var(--text-color-grey);
        margin: 0;
    }
    .card .links {
        margin-top: 32px;
    }
    .card a {
        padding: 8px 24px;
        border: solid 1px var(--text-color-black);
        border-radius: 12px;
        text-decoration: none;
        color: var(--text-color-black);
        display: inline-block;
        margin-right: 8px;
    }
    .card a:first-child {
        color: #fff;
        background-color: var(--text-color-black);
    }
</style>