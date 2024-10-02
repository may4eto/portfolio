<script>
    import { createEventDispatcher } from 'svelte';
    export let data
    export let filteredProjects
    export let selected
    const dispatch = createEventDispatcher();
    const projectTags = data.projects.map(project => project.tags.toString()).toString().split(",").sort()
    const uniqueTags = [...new Set(projectTags)]
    let onFilterProjects = (event) => {
        dispatch('filter', {
			text: event.target.innerHTML,
            id: event.target.getAttribute('id')
		});
    }
    let onClearFilters = () => {
        dispatch('clear', {})
    }
</script>
<div class="card">
    <div class="title">
        <h2>
            {#if filteredProjects.length > 0}
                Projects <span class="badge"><span class="projects-count">{filteredProjects.length}</span></span>
            {:else}
                Projects <span class="badge"><span class="projects-count">{data.projects.length}</span></span>
            {/if}
        </h2>
        {#if filteredProjects.length > 0}
            <button on:click={onClearFilters}>Clear filters<span class="close material-symbols-rounded">close</button>
        {/if}
    </div>
    <div class="tags">
        {#each uniqueTags as tag, index (index)}  
            <span id={index.toString()} on:click = {onFilterProjects} class:selected="{selected === index.toString()}">
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
    .card .title {
        display: flex;
        align-items: center;
    }
    .card .title button {
        margin: 0 0 12px 12px;
        font-family: inherit;
        font-size: 14px;
        padding: 8px 12px;
        border-radius: 12px;
        box-sizing: border-box;
        border: none;
        appearance: none;
        cursor: pointer;
    }
    .card .title div:hover {
        background-color: var(--text-color-grey);
        color: #fff;
    }
    .card .title span.close {
        font-size: 14px;
    }
    .card .title span.projects-count {
        font-variant-numeric: tabular-nums;
    }
    .card .title span.close {
        margin-left: 4px;
        display: inline-block;
        vertical-align: middle;
        padding: 0;
    }
    .card .title h2 {
        display: flex;
        margin-bottom: 12px;
    }
    .card .tags {
        display: flex;
        flex-wrap: wrap;
    }
    .card .tags span {
        padding: 8px 16px;
        border: solid 1px var(--text-color-black);
        border-radius: 12px;
        margin: 8px 8px 0 0;
        display: inline-block;
        cursor: pointer;
    }

    span.badge {
        background-color: var(--light-grey);
        display: flex;
        align-items: center;
        justify-content: center;
        width: 16px;
        height: 16px;
        padding: 8px;
        border-radius: 50%;
        margin-left: 8px;
    }

    span.projects-count {
        font-size: 16px;
    }

    @media (max-width: 375px) {
        .card {
            margin-bottom: 16px;
        }
}
</style>
