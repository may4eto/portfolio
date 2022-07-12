<script>
  import ProfileCard from './lib/ProfileCard.svelte'
  import SkillsCard from './lib/SkillsCard.svelte'
  import HobbiesCard from './lib/HobbiesCard.svelte'
  import ExperienceCard from './lib/ExperienceCard.svelte'
  import BlogCard from './lib/BlogCard.svelte'    
  import ProjectsCard from './lib/ProjectsCard.svelte';
  import ProjectGrid from './lib/ProjectGrid.svelte';
  import { onMount } from "svelte";
import Footer from './lib/Footer.svelte'
  let blogData = []
  onMount(async () => {
        const response = await fetch(
                'https://dev.to/api/articles?username=may4eto',
                {
                    method: 'GET',
                }
            );
            const data = await response.json();
            blogData = data[0]
            console.log(blogData)
  });
  let data =  {
    name: "Maya Mircheva",
    role: "Front-end developer",
    email: "maya.p.mircheva@gmail.com",
    telephone: "+39 351 664 31 82",
    description: "A multidisciplinary creative skilled in project management, graphic design, web design and web development. Experienced in working in an international environment. Passionate about using technology and design for making the world a better place. A wannabe artist. Multilingual. Lifelong learner.",
    socials: [
      { name: "linkedin", url: "https://www.linkedin.com/in/mayamircheva/" },
      { name: "github", url: "https://github.com/may4eto" },
      { name: "dribbble", url: "https://dribbble.com/maya_mircheva" },
      { name: "behance", url: "https://www.behance.net/maya516592f0b9" }
    ],
    skills: [
      { name: "HTML", mastery: "80%"},
      { name: "CSS", mastery: "80%"},
      { name: "JavaScript", mastery: "60%"},
      { name: "Svelte", mastery: "40%"},
      { name: "React", mastery: "60%"},
      { name: "Vue", mastery: "40%"},
      { name: "Angular", mastery: "60%"},
      { name: "UX/UI", mastery: "80%"}
    ],
    hobbies: [
      { name: "Art", description: "From drawing and painting to applied arts, I love all things creative.", image: "art.jpg"},
      { name: "Reading", description: "I am not much of a book worm but I love curling up with a good book.", image: "reading.jpg"},
      { name: "Dancing", description: "I enjoy social dancing, in particular tango, balboa and swing.", image: "tango.jpg"}
    ],
    experiences: [
      { dates: "2021-current", role: "Front-end developer", description: "Development of a web application with Angular", image: "avanade.png" },
      { dates: "2020", role: "Full-stack developer", description: "Development of a web application for a small retail client with Laravel and MySQL", image: "nowhere.png" },
      { dates: "2020", role: "Web designer", description: "Graphic and web design work in Adobe XD and Adobe Illustrator for various clients", image: "2create.png" },
      { dates: "2013-2019", role: "Assistant", description: "Various administrative, paralegal and policy support roles at EU institutions and agencies", image: "eu.png" },
      // { dates: "2010-2013", role: "Project coordinator", description: "Funding and capacity building for NGOs", image: "osf.png" }
    ],
    projects: [
      { name: "Book Club", image: "bookclub.png", url: "https://book-club-app.netlify.app", repo: "https://github.com/may4eto/book-club", description: "A responsive website fetching data from an external API and using React hooks and the styled-components library.", tags: ["React", "HTML", "CSS"] },
      { name: "Zesty", image: "zesty.png", url: "https://zesty.netlify.app", repo: "https://codesandbox.io/s/zesty-t0dqh", description: "A responsive photography portfolio implementing a simple carrousel functionality with React hooks and CSS.", tags: ["React", "HTML", "CSS"] },  
      { name: "MilkyMood", image: "milkymood.png", url: "https://milkymood.netlify.app", repo: "https://codesandbox.io/s/milkymood-p03jo", description: "A landing page for an indie album pre-release using React hooks, Formik and the styled-components libraries. ", tags: ["React", "HTML", "CSS"] },
      { name: "Edie", image: "edie.png", url: "https://may4eto.github.io/edie-homepage/", repo: "https://github.com/may4eto/edie-homepage", description: "A static responsive business home page created with HTML and CSS exploring different styles of CSS grid.", tags: ["HTML", "CSS"] },
      { name: "Fitra", image: "fitra.png", url: "https://maya-mircheva-superhi-project-1.myshopify.com/", repo: "https://github.com/may4eto/fitra", description: "*DEMO STORE, NO ORDERS - password: superhi* <br> A single-page Shopify custom theme", tags: ["Shopify", "CSS"] },
      { name: "Wellby", image: "wellby.png", url: "https://maya-mircheva-superhi-project-2.myshopify.com/", repo: "https://github.com/may4eto/wellby", description: "*DEMO STORE, NO ORDERS - password: superhi* <br> A multi-page Shopify custom theme", tags: ["Shopify", "CSS"] },
    ]
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
      <ProjectsCard {data} />
      <ProjectGrid {data} />
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
