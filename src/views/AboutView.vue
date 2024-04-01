<template>
  <div class="contact">
    <!--<transition appear name="fade" @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter" @before-leave="beforeLeave" @leave="leave" @after-leave="afterLeave">
      <h1 v-if="showTitle">Contactame</h1>
    </transition>-->

    <transition appear name="fade" @before-enter="beforeEnter" @enter="enter">
      <h1>Contactame</h1>
    </transition>
    
    <ul>
      <li v-for="icon in icons" :key="icon.name">
        <span class="material-icons">{{ icon.name }}</span>
        <div>{{ icon.text }}</div>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const icons = ref([
  { name: 'alternate_email', text: 'by email'},
  { name: 'local_phone', text: 'by phone'},
  { name: 'local_post_office', text: 'by post'},
  { name: 'local_fire_department', text: 'by smoke signal'},
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

const beforeEnter = (el) => {

}

const enter = (el) => {

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
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    cursor: pointer;
    line-height: 1.5em;
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
