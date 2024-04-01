<template>
  <div class="todos">
    <input 
      type="text" 
      v-model="newTodo" 
      @keypress.enter="addTodo"
      placeholder="Agrega una nueva tarea..."
    />

    <transition name="switch" mode="out-in">
      <div v-if="todos.length">
        <transition-group name="list" tag="ul" appear>
          <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
            {{ todo.text }}
          </li>
        </transition-group>
      </div>
      <div v-else>No hay tareas por hacer!</div>
    </transition>
  </div>
</template>
  
<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits(['badValue'])

const todos = ref([])

const newTodo = ref('')

const addTodo = () => {
    if (newTodo.value) {
        const id = Math.random()
        todos.value = [{ text: newTodo.value, id }, ...todos.value]
        newTodo.value = ''
    } else {
        emit('badValue')
    }
}

const deleteTodo = (id: number) => {
    todos.value = todos.value.filter(todo => todo.id != id)
}
</script>
  
<style>
  .todos {
    max-width: 400px;
    margin: 20px auto;
    position: relative;
  }

  input {
    width: 100%;
    padding: 12px;
    border: 1px solid #66FCF1;
    border-radius: 10px;
    box-sizing: border-box;
    margin-bottom: 20px;
    background-color: #0B0C10;
    color: white;
  }

  input:focus {
    background-color: white;
    color: black;
  }

  .todos ul {
    position: relative;
    padding: 0;
  }
  
  .todos li {
    list-style-type: none;
    display: block;
    margin-bottom: 10px;
    padding: 10px;
    background: #0B0C10;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    border-radius: 10px;
    border: 1px solid #66FCF1;
    width: 100%;
    box-sizing: border-box;
    color: white;
  }
  
  .todos li:hover {
    cursor: pointer;
  }

  /* List transition */
  .list-enter-from {
    opacity: 0;
    transform: scale(0.6);
  }

  .list-enter-to {
    opacity: 1;
    transform: scale(1);
  }

  .list-enter-active {
    transition: all .4s ease;
  }

  .list-leave-from {
    opacity: 1;
    transform: scale(1);
  }

  .list-leave-to {
    opacity: 0;
    transform: scale(0.6);
  }

  .list-leave-active {
    transition: all .4s ease;
    position: absolute;
  }

  .list-move {
    transition: all .3s ease;
  }

  /* Switch transitions */
  .switch-enter-from,
  .switch-leave-to {
    opacity: 0;
    transform: translateY(20px);
  }

  .switch-enter-active,
  .switch-leave-active {
    transition: all .5s ease;
  }
</style>