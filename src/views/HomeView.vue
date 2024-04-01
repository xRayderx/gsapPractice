<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Toast from '../components/ToastComponent.vue'
import Todos from '../components/TodoComponent.vue'

const showToast = ref(false)
const showP = ref(false)

const triggerToast = () => {
  showToast.value = true;
  setTimeout(() => showToast.value = false, 3000)
}
</script>

<style>
  /*.toast-enter-from {
    opacity: 0;
    transform: translateY(-60px);
  }
  
  .toast-enter-to {
    opacity: 1;
    transform: translateY(0)
  }
  */
  
  .toast-enter-active {
    /*transition: all .3s ease-in;*/
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