<script>
  import { writable } from 'svelte/store';
  import { data } from './data.js'
  import ProfileCard from './lib/ProfileCard.svelte'
  import SkillsCard from './lib/SkillsCard.svelte'
  import HobbiesCard from './lib/HobbiesCard.svelte'
  import ExperienceCard from './lib/ExperienceCard.svelte'
  import BlogCard from './lib/BlogCard.svelte'    
  import ProjectsCard from './lib/ProjectsCard.svelte';
  import ProjectGrid from './lib/ProjectGrid.svelte';
  import Footer from './lib/Footer.svelte'
  import P5 from 'p5-svelte';

  const isReady = writable()
  isReady.set(false) 
  let _isReady
  isReady.subscribe((value) => {
    _isReady = value
  });
  let blogData = []
  let filterTerm = ""
  let filteredProjects = []
  let selected= ""
  const fetchData = (async () => {
    const response = await fetch('https://dev.to/api/articles?username=may4eto', {method: "GET"})
    const data = await response.json()
    blogData = data[0]
  })
  //onMount(fetchData);

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

  let words
  let position
  let wordList
  let wordNum
  let nl
  let canvasHeight
  let canvasWidth
  let totalX
  let totalY
  let density
  let sketch

  const htmlTag = document.querySelector("html")

  isReady.subscribe(value => {
    if (value) {
    sketch = (p5) => {
      p5.setup = () => {
        nl = 0.0025
        density = 5
        canvasHeight = htmlTag.scrollHeight
        canvasWidth = htmlTag.clientWidth
        totalX = canvasWidth
        totalY = canvasHeight
        let c1 = p5.color("#c4c4c4")
        let c2 = p5.color("#828282")
        p5.createCanvas(canvasWidth, canvasHeight)
        for(let x = 0; x < totalX; x = x + 1 ) {
          for(let y = 0; y < totalY; y = y + 1) {
            let n = p5.noise(x * nl, y * nl)
            let rn = n * density - p5.floor(n * density)
            //let c = p5.lerpColor(c1, c2, rn)
            let c = c2
            if(rn > 0.75) {
              c = c1
            }
            p5.set(x, y, c)
          }
        }
        p5.updatePixels()
      }
      return sketch
    }
  } else {
    // splash screen 
    sketch = (p5) => {
      let easing = function (t) { return t*t*t }

      class Word {
        constructor(x, y, text) {
          let randomAngle = p5.random(-0.25 * p5.PI, 0.25 * p5.PI)
          this.position = p5.createVector(x, y)
          this.speed = p5.createVector(0, -10)
          this.speed = this.speed.rotate(randomAngle)
          this.acc = p5.createVector(0, 0.5)
          this.friction = 0.99
          this.elastic = 0.8
          this.time = 0
          this.text = text
        }
        move() {
          this.speed = this.speed.add(this.acc)
          this.speed = this.speed.mult(this.friction)
          this.position = this.position.add(this.speed)
          if (this.position.y > htmlTag.clientHeight) {
            this.speed.y = this.speed.y * -1 * this.elastic
          }
          this.position.y = p5.constrain(this.position.y, -1000, htmlTag.clientHeight)
          this.time = this.time + 0.005
        }
        draw() {
          this.move()
          let alpha = 255 - 255 * easing(this.time)
          htmlTag.clientWidth < 768 ? p5.textSize(80) : p5.textSize(160)
          p5.fill(255, 255, 255, alpha)
          p5.noStroke()
          p5.textFont("Montserrat")
          p5.textAlign(p5.CENTER, p5.BASELINE)
          p5.text(this.text, this.position.x, this.position.y)
        }
      }

      p5.setup = () => {
        p5.createCanvas(htmlTag.clientWidth, htmlTag.clientHeight)
        words = []
        wordList = ["Maya", "is", "a", "designer", "an", "artist", "and", "a", "creative", "coder"]
        wordNum = 0
        position = p5.createVector(100, 300)
        setTimeout(writeWord, 700);
      }
      p5.draw = () => {
          p5.background("#000000")
          words.forEach(w => {
            w.draw()
          })
          p5.updatePixels()
        }
      function writeWord() {
        let choice = wordList[wordNum]  
        let w = new Word(p5.random(htmlTag.clientWidth / 2 - 50, htmlTag.clientWidth / 2 + 50), htmlTag.clientHeight / 2, choice)
        words.push(w)
        wordNum = wordNum + 1
        setTimeout(writeWord, 700);
        if (wordNum === wordList.length - 1) {
          setTimeout(() => {
            isReady.update((isReady) => isReady = true)
            p5.noCanvas()
            fetchData()
          }, 7000)
          clearTimeout(0)
        }
      }
      return sketch
    }
  }
  })
</script>

{#if _isReady}
  <main>
    <ProfileCard {data} />
    <section class="intro">
      <SkillsCard {data} />
      <BlogCard {blogData}/>
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
  <P5 {sketch} />
{/if}
<P5 {sketch} />

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
