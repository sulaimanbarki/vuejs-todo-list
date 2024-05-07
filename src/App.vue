<template>
  <main>
    <Header />

    <AddToDo @addToDoItem="handleAddTodoItem" />

    <ToDoList :todoList="todoList" @updateTodoList="handleUpdateToDoList" @deleteItem="handleDeleteItem"/>
  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import uniqid from 'uniqid';
import { useToast } from 'vue-toastification';



import Header from './components/Header.vue';
import AddToDo from './components/AddToDo.vue';
import ToDoList from './components/ToDoList.vue';

const todoList = ref([]);
const toaster = useToast();

const handleAddTodoItem = (item) => {
  todoList.value.push({
    id: uniqid(),
    text: item.text,
    isDone: false
  })

  toaster.success('Todo item added successfully');

  saveToLocalStorage();
}

// add todoList to localStorage
function saveToLocalStorage() {
  localStorage.setItem('todoList', JSON.stringify(todoList.value));
}

// onmounted get todoList from localStorage
function getFromLocalStorage() {
  const savedList = localStorage.getItem('todoList');
  if (savedList) {
    todoList.value = JSON.parse(savedList);
  }
}

onMounted(() => {
  getFromLocalStorage();
})

const handleUpdateToDoList = (id) => {
  const index = todoList.value.findIndex((item) => item.id === id);
  todoList.value[index].isDone = !todoList.value[index].isDone;

  toaster.success('Todo item updated successfully');

  saveToLocalStorage();
}

const handleDeleteItem = (id) => {
  const index = todoList.value.findIndex((item) => item.id === id);
  todoList.value.splice(index, 1);

  toaster.success('Todo item deleted successfully');

  saveToLocalStorage();
}


</script>

<style scoped>

main {
  height: 100vh;
  width: 600px;
  background-color: #EEEEEE;
  margin: 0px auto;
  padding: 20px;
}
</style>
