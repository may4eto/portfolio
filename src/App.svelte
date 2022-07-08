<script>
  import ProfileCard from './lib/ProfileCard.svelte'
  import SkillsCard from './lib/SkillsCard.svelte'
  import HobbiesCard from './lib/HobbiesCard.svelte'
  import ExperienceCard from './lib/ExperienceCard.svelte'
  import BlogCard from './lib/BlogCard.svelte'    
  import { onMount } from "svelte";
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
      { dates: "2021-current", role: "Front-end developer", description: "Development of web applications with Angular", image: "avanade.png" },
      { dates: "2020", role: "Full-stack developer", description: "Development of web applications with Laravel and MySQL", image: "nowhere.png" },
      { dates: "2020", role: "Web designer", description: "Graphic and web design work in Adobe XD and Adobe Illustrator", image: "2create.png" },
      { dates: "2013-2019", role: "Assistant", description: "Various administrative, paralegal and policy support roles", image: "eu.png" },
      // { dates: "2010-2013", role: "Project coordinator", description: "Funding and capacity building for NGOs", image: "osf.png" }
    ]
  }
</script>

{#if blogData}
  <main>
    <ProfileCard data={data} />
    <div class="intro">
      <SkillsCard data={data} />
      <BlogCard blogData={blogData} />
      <HobbiesCard data={data} />
      <ExperienceCard data={data} />
    </div>
    <div class="projects"></div>
  </main>
{:else}
  ...loading
{/if}

<style>
  div.intro {
    display: grid;
    grid-template-columns: 40fr 60fr;
    gap: 24px;
    margin: 24px 0;
  }
</style>
