<script>
    import { createEventDispatcher } from 'svelte';
    export let data
    export let filteredProjects
    const dispatch = createEventDispatcher();
    const projectTags = data.projects.map(project => project.tags.toString()).toString().split(",").sort()
    const uniqueTags = [...new Set(projectTags)]
    let onFilterProjects = (event) => {
        dispatch('filter', {
			text: event.target.innerHTML
		});
    }
</script>
<div class="card">
    <h2>
        {#if filteredProjects.length > 0}
            Projects ( {filteredProjects.length} )
        {:else}
            Projects ( {data.projects.length} )
        {/if}
    </h2>
    <div class="tags">
        {#each uniqueTags as tag}  
            <span on:click = {onFilterProjects} >
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
        cursor: pointer;
    }
    .card span .selected {
        background-color: var(--text-color-black);
        color: #fff;
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
