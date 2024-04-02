<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>

    <transition appear @before-enter="beforeEnter" @enter="enter">
      <h1>Todo App</h1>
    </transition>
    
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import gsap from 'gsap'
import Toast from '../components/ToastComponent.vue'
import Todos from '../components/TodoComponent.vue'

const showToast = ref(false)

const triggerToast = () => {
  showToast.value = true;
  setTimeout(() => showToast.value = false, 3000)
}

const beforeEnter = (el: any) => {
  el.style.transform = 'translateY(-60px)'
  el.style.opacity = 0
}

const enter = (el: any, done: any) => {
  gsap.to(el, {
    duration: 3,
    y: 0,
    opacity: 1,
    ease: 'bounce.out',
    onComplete: done
  })
}
</script>

<style>
  .toast-enter-active {
    animation: wobble .5s ease;
  }

  .toast-leave-from {
    opacity: 1;
    transform: translateY(0);
  }

  .toast-leave-to {
    opacity: 0;
    transform: translateY(-60px);
  }

  .toast-leave-active {
    transition: all .3s ease;
  }

  @keyframes wobble {
    0% {
      opacity: 0;
      transform: translateY(-60px);
    }
    50% {
      opacity: 1;
      transform: translateY(0);
    }
    60% {
      transform: translateX(8px);
    }
    70% {
      transform: translateX(-8px);
    }
    80% {
      transform: translateX(4px);
    }
    90% {
      transform: translateX(-4px);
    }
    100% {
      transform: translateX(0);
    }
  }
</style>