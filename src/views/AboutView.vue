<template>
  <div class="contact">
    <!--<transition appear name="fade" @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter" @before-leave="beforeLeave" @leave="leave" @after-leave="afterLeave">
      <h1 v-if="showTitle">Contactame</h1>
    </transition>-->

    <transition appear @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter">
      <h1>Contactame</h1>
    </transition>
    
    <transition-group tag="ul" appear @before-enter="beforeEnterIcon" @enter="enterIcon">
      <li v-for="(icon, index) in icons" :key="icon.name" :data-index="index">
        <a :href="icon.link" rel="noreferrer noopener">
          <span class="material-icons">{{ icon.name }}</span>
          <div>{{ icon.text }}</div>
        </a>
      </li>
    </transition-group>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import gsap from 'gsap'

const icons = ref([
  { name: 'computer', text: 'Github', link: 'https://github.com/xRayderx'},
  { name: 'send', text: 'Telegram', link: 'https://t.me/xRayder18'},
  { name: 'work', text: 'Linkedin', link: 'https://www.linkedin.com/in/josemarti1896/'},
  { name: 'mail', text: 'Correo', link: 'mailto:josemarti1896@gmail.com'}
])

/*const showTitle = ref(true)

const beforeEnter = (el) => {
  console.log("Antes de entrar", el)
}

const enter = (el) => {
  console.log("Entramos", el)
}

const afterEnter = (el) => {
  el.style.color = 'green'
  console.log("Despues de entrar", el)
  
  setTimeout(() => showTitle.value = false, 2000);
}

const beforeLeave = (el) => {
  el.style.color = 'pink'
  console.log("Antes de salir", el)
}

const leave = (el) => {
  console.log("Salimos", el)
}

const afterLeave = (el) => {
  console.log("Despues de salir", el)
}*/

const beforeEnter = (el: any) => {
  console.log("Antes de entrar - estado inicial")
  el.style.transform = 'translateY(-60px)'
  el.style.opacity = 0
}

const enter = (el: any, done: any) => {
  console.log("Entramos - haz la transición")
  gsap.to(el, {
    duration: 3,
    y: 0,
    opacity: 1,
    ease: 'bounce.out',
    onComplete: done
  })
}

const afterEnter = () => {
  console.log("Despues de entrar")
}

const beforeEnterIcon = (el: any) => {
  console.log("Antes de entrar iconos")

  el.style.opacity = 0;
  el.style.transform = 'translateY(100px)'
}

const enterIcon = (el: any, done: any) => {
  console.log("Entran iconos")
  gsap.to(el, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    onComplete: done,
    delay: el.dataset.index * 0.2
  })
}
</script>

<style>
  .contact ul {
    padding: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    max-width: 400px;
    margin: 60px auto;
  }

  .contact li {
    list-style-type: none;
    background: #0B0C10;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    cursor: pointer;
    line-height: 1.5em;
    color: white;
    border: 1px solid #66FCF1;
  }

  a {
    text-decoration: none;
  }

  a:visited {
    color: white;
  }

  a[href^="mailto"] {
    color: white;
  }

  a[href^="mailto"]:visited {
    color: white;
  }

  .fade-enter-from { 
    opacity: 0;
  }

  .fade-enter-active {
    transition: opacity 3s ease;
  }

  .fade-leave-to {
    opacity: 0;
  }

  .fade-leave-active {
    transition: opacity 3s ease;
  }
</style>
