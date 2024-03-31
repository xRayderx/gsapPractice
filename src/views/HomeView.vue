<template>
  <div class="home">
    <Toast v-if="showToast" />
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Toast from '../components/ToastComponent.vue'
import Todos from '../components/TodoComponent.vue'

const showToast = ref(false)

const triggerToast = () => {
  showToast.value = true;
  setTimeout(() => showToast.value = false, 3000)
}
</script>