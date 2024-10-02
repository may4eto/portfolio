<script>
  import { onMount } from "svelte";
  import { data } from './data.js'
  import ProfileCard from './lib/ProfileCard.svelte'
  import SkillsCard from './lib/SkillsCard.svelte'
  import HobbiesCard from './lib/HobbiesCard.svelte'
  import ExperienceCard from './lib/ExperienceCard.svelte'
  import BlogCard from './lib/BlogCard.svelte'    
  import ProjectsCard from './lib/ProjectsCard.svelte';
  import ProjectGrid from './lib/ProjectGrid.svelte';
  import Footer from './lib/Footer.svelte'
  let blogData = []
  let filterTerm = ""
  let filteredProjects = []
  let selected= ""
  onMount(async () => {
        const response = await fetch(
                'https://dev.to/api/articles?username=may4eto',
                {
                    method: 'GET',
                }
            );
            const data = await response.json();
            blogData = data[0]
  });
  //filter function
  const filterProjects = (event) => {
    filterTerm = `${event.detail.text.trim()}`
    selected = event.detail.id
    filteredProjects = data.projects.filter(project => project.tags.includes(filterTerm))
  }
  //clear filters
  const clearFilters = () => {
    filteredProjects = []
    selected = ""
  }
</script>

{#if blogData}
    <main>
      <ProfileCard {data} />
      <section class="intro">
        <SkillsCard {data} />
        <BlogCard {blogData} />
        <HobbiesCard {data} />
        <ExperienceCard {data} />
      </section>
      <section class="projects">
        <ProjectsCard {data} {filteredProjects} {selected} on:filter={filterProjects} on:clear={clearFilters}/>
        {#key filteredProjects}
          <ProjectGrid {data} {filteredProjects} />
        {/key}
      </section>
    </main>
    <Footer />
{:else}
  ...loading
{/if}

<style>
  @import '../src/assets/global.css';
  section.intro {
    display: grid;
    grid-template-columns: 40fr 60fr;
    gap: 24px;
    margin: 24px 0;
    align-items: start;
  }
  @media (max-width: 1024px) {
    section.intro {
      gap: 16px;
    }
  }
  @media (max-width: 986px) {
    section.intro {
      grid-template-columns: 50fr 50fr;
    }
  }
  @media (max-width: 950px) {
    section.intro {
      grid-template-columns: 1fr;
      gap: 24px;
    }
  }
  @media (max-width: 375px) {
    section.intro {
      gap: 16px;
      margin: 16px 0;
    }
  }
</style>
