<script>
    import ProjectCard from './ProjectCard.svelte' 
    export let data
</script>

<div class="projects-grid">
    {#each data.projects as project}
        <ProjectCard {project} />
    {/each}
</div>

<style>
    .projects-grid {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 24px;
}
</style>