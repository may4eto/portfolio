<script>
    export let data
    const projectTags = data.projects.map(project => project.tags.toString()).toString().split(",")
    const uniqueTags = [...new Set(projectTags)]
</script>
<div class="card">
    <h2>
        Projects ( {data.projects.length} )
    </h2>
    {#each uniqueTags as tag}  
        <span>
            {tag}
        </span>
    {/each}
</div>
<style>
    .card {
        max-width: 1024px;
        margin-bottom: 24px;
    }
    .card span {
        padding: 8px 16px;
        border: solid 1px var(--text-color-black);
        border-radius: 12px;
        margin-right: 8px;
    }
</style>
