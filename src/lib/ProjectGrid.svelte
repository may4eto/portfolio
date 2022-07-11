<script>
    import { paginate, LightPaginationNav } from 'svelte-paginate'
    import ProjectCard from './ProjectCard.svelte' 
    export let data
    let items = [...data.projects]
    let currentPage = 1
    let pageSize = 3
    $: paginatedItems = paginate({ items, pageSize, currentPage })
</script>

<div class="projects-grid">
    {#each paginatedItems as item}
    <div class="item">
      <ProjectCard project={item} />
    </div>
  {/each}
</div>
<div class="pagination">
    <LightPaginationNav
    totalItems="{items.length}"
    pageSize="{pageSize}"
    currentPage="{currentPage}"
    limit="{3}"
    showStepOptions="{true}"
    on:setPage="{(e) => currentPage = e.detail.page}"
/>
</div>

<style>
    .projects-grid {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 24px;
    }
    .pagination :global(.pagination-nav) {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 24px;
        background-color: transparent;
        -webkit-box-shadow: none;
        box-shadow: none;
        border-radius: 0;
        box-sizing: border-box;
    }
    .pagination :global(.option) {
        display: inline-block;
        vertical-align: middle;
        color: var(--text-color-grey);
    }
    .pagination :global(.option.active) {
        background-color: var(--text-color-grey);
        border: 1px solid var(--text-color-grey);
        color: #fff;
    }
    .pagination :global(.option.number) {
        border: 1px solid var(--text-color-grey);
        padding: 4px 8px;
        border-radius: 4px;
        font-variant-numeric: tabular-nums;
    }
    .pagination :global(.option.number:not(:first-child)) {
        margin-left: 8px;
    }
    .pagination :global(.option svg path) {
        fill: var(--text-color-black);
    } 
</style>