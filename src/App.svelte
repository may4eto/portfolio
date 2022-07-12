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
    filterTerm = `${event.detail.text.trim()}`;
    return filteredProjects = data.projects.filter(project => project.tags.includes(filterTerm))
  }
</script>

{#if blogData}
  <main>
    <ProfileCard {data} />
    <div class="intro">
      <SkillsCard {data} />
      <BlogCard {blogData} />
      <HobbiesCard {data} />
      <ExperienceCard {data} />
    </div>
    <div class="projects">
      <ProjectsCard {filteredProjects} {data} on:filter={filterProjects} />
      <ProjectGrid {data} {filteredProjects} />
    </div>
  </main>
  <Footer />
{:else}
  ...loading
{/if}

<style>
  @import '../src/assets/global.css';
  div.intro {
    display: grid;
    grid-template-columns: 40fr 60fr;
    gap: 24px;
    margin: 24px 0;
    align-items: start;
  }
  @media (max-width: 1024px) {
    div.intro {
      gap: 16px;
    }
  }
  @media (max-width: 986px) {
    div.intro {
      grid-template-columns: 50fr 50fr;
    }
  }
  @media (max-width: 950px) {
    div.intro {
      grid-template-columns: 1fr;
      gap: 24px;
    }
  }
  @media (max-width: 375px) {
    div.intro {
      gap: 16px;
      margin: 16px 0;
    }
  }
</style>
