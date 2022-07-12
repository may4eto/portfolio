<script>
    export let data
    const projectTags = data.projects.map(project => project.tags.toString()).toString().split(",")
    const uniqueTags = [...new Set(projectTags)]
</script>
<div class="card">
    <h2>
        Projects ( {data.projects.length} )
    </h2>
    <div class="tags">
        {#each uniqueTags as tag}  
            <span>
                {tag}
            </span>
        {/each}
    </div>
</div>
<style>
    .card {
        max-width: 1024px;
        margin-bottom: 24px;
    }
    .card h2 {
        margin-bottom: 12px;
    }
    .card span {
        padding: 8px 16px;
        border: solid 1px var(--text-color-black);
        border-radius: 12px;
        margin: 8px 8px 0 0;
        display: inline-block;
    }
    .card .tags {
        display: flex;
        flex-wrap: wrap;
    }
    @media (max-width: 375px) {
        .card {
            margin-bottom: 16px;
        }
}
</style>
