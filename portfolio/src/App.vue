
<script setup>
import './assets/style.css'
import { ref, useTemplateRef, computed  } from 'vue'
import { useElementBounding } from '@vueuse/core'
 // // :style="{ mask: `radial-gradient(circle at ${offsetX}px ${offsetY}px, white 10%, rgba(0, 0, 0, 0.5) 50%)` }"
  const image = useTemplateRef('logo')
  const { x, y, top, right, bottom, left, width, height } = useElementBounding(image)
  const offsetY = ref(0)
  const offsetX = ref(0)
  const isHovering = ref(false)

  function onMousemove(e) {
    offsetX.value = e.clientX - left.value
    offsetY.value = e.clientY - top.value
    isHovering.value = true
    console.log("returned")
  }

  function onMouseleave() {
    isHovering.value = false
    console.log("left")
  }

  const logoStyle = computed(() => {
  if (isHovering.value) {
    return {
      mask: `radial-gradient(circle at ${offsetX.value}px ${offsetY.value}px, white 10%, rgba(0, 0, 0, 0.5) 50%)`,
      transition: 'mask 1s ease-out'
    }
  } else {
    return {
      transition: 'opacity 1s ease-out',
      opacity: 0.3
    }
  }
  
})
</script>

<template>
  <header>
    <div class="wrapper">
      <h1><span style="color:#d79921">euan@software-engineer</span>:<span style="color:#458588">~</span>$ ls ./WelcomePage</h1>
      <div class="links">
        <h3><a href="">Home.html</a></h3>
        <h3><a href="">About.html</a></h3>
        <h3><a href="">Pojects.html</a></h3>
        <h3>Intro.py</h3>
      </div>
      <h1><span style="color:#d79921">euan@software-engineer</span>:<span style="color:#458588">~</span>$ python ./Intro.py</h1>
      <div class="intro">
        <h3>Software Engineer <span style="color:#cc241d">@</span> FutureRoots Enterprise</h3>
        <h3>MSc Agricultural Technology & Innovation <span style="color:#cc241d">@</span> RAU</h3>
        <h3>BSc Computer Science <span style="color:#cc241d">@</span> Loughborough</h3>
        <br><h3>Featured Projects:</h3>
        <h3><a href="">FutureRoots.app</a></h3>
        <h3><a href="">Morris.web</a></h3>

        <br>
        <div class="links">
          <h3><a href="">GitHub</a></h3>
          <h3><a href="">LinkedIn</a></h3>
          <h3><a href="">YouTube</a></h3>
        </div>
      </div>
    </div>

    
  </header>
  <div class="images">
      <img  ref="logo" 
      @mousemove="onMousemove"
      @mouseleave="onMouseleave":style="logoStyle"
      alt="ASCII Fern" class="logo" src="./assets/fern.svg" width="90%" height="auto" />
      
      <img alt="ASCII Fern" class="me" src="./assets/me.svg" width="40%" height="auto" />
    </div>
  <main>
  </main>
</template>

<style scoped>
header {
  line-height:1.5;
}

.wrapper{
  min-height: 200px;
  margin:0;
  padding:10px;
}

.wrapper .links {
  padding:5px; 
  margin-right: 10rem;
  display: inline-block;
  display:flex;   
  justify-content: space-between;
  flex-flow:row wrap;
}

@media (min-width: 1024px) {
  header {
    place-items: center;
    margin-top: 4rem;
  }

  .logo {
    translate: 0% 60%
  }
  .me {
    display: flex;
    place-items: flex-start;
    translate: 75% -155%;
  }
  .images {
    display: inline-flexbox;
  }

  .wrapper{
    font-family: "JetBrains Mono";
  }
}
</style>

