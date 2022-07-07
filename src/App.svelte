<script>
  import ProfileCard from './lib/ProfileCard.svelte'
  let data =  {
    name: "Maya Mircheva",
    role: "Front-end developer",
    email: "maya.p.mircheva@gmail.com",
    telephone: "+39 351 664 31 82",
    description: "A multidisciplinary creative skilled in project management, graphic design, web design and web development. Experienced in working in an international environment. Passionate about using technology and design for making the world a better place. A wannabe artist. Multilingual. Lifelong learner.",
  }
</script>

<main>
  <ProfileCard data={data} />
</main>

<style>
  
</style>
