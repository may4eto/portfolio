<script>
    import { paginate, LightPaginationNav } from 'svelte-paginate'
    import ProjectCard from './ProjectCard.svelte' 
    export let data
    export let filteredProjects
    let items = filteredProjects.length > 0 ? [...filteredProjects] : [...data.projects]
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
        color: var(--text-color-black);
        padding: 8px;
    }
    .pagination :global(.option.active) {
        background-color: var(--text-color-black);
        border: 1px solid var(--text-color-black);
        color: #fff;
    }
    .pagination :global(.option.number) {
        border: 1px solid var(--text-color-black);
        border-radius: 4px;
        font-variant-numeric: tabular-nums;
        margin: 0 4px;
    }
    .pagination :global(.option.prev svg path),
    .pagination :global(.option.next svg path){
        fill: var(--text-color-black);
    } 
    .pagination :global(.option.prev.disabled svg path),
    .pagination :global(.option.next.disabled svg path){
        fill: var(--text-color-grey);
    } 
    @media (max-width: 1024px) {
        .projects-grid {
            gap: 16px;
        }
    }
    @media(max-width:950px) {
        .projects-grid {
            grid-template-columns: 1fr;
            gap: 24px;
        }
    }
    @media (max-width: 375px) {
        .projects-grid {
            gap: 16px;
        }
    }
</style>