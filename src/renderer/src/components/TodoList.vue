<script setup>
import { AkPlus } from "@kalimahapps/vue-icons";
import { ref } from "vue";
import { AnFilledDelete } from "@kalimahapps/vue-icons";




//Vue prime library
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';


const newTodo = ref(""); // two-way binding

// Khoi taoj mang todo

const todos = ref([
  { status: false, data: "Buy a new gaming laptop" },
  { status: false, data: "Lean vue 3" },
  { status: false, data: "Read a book" },
]);

//handle add todo
const addTodo = () => {
  const data = newTodo.value.trim();
  if (data) {
    todos.value.push({status: false, data});
    newTodo.value = "";
  }
};

//handle toggle delete button
const toggleShowDeleteButton = (index) => {

    todos.value[index].status = !todos.value[index].status
}
//handle delete todo 
const handleClickTodo = (index) => {
    todos.value.splice(index,1)
}

//handle clear all todo
const clearAllTodo = () => {
    todos.value = []
}
</script>

<template>
  <div class="flex justify-center items-center bg-gradient w-screen h-screen">
    <div class="flex flex-col h-3/5 w-4/5 bg-white lg:w-3/12 lg:h-2/3 p-5 space-y-3">
      <h1 class="font-bold text-2xl sm:text-3xl">Todo App</h1>
      <div class="flex space-x-2">
        <InputText
          v-model="newTodo"
          class="border border-[#c3a9f5] h-9 w-full px-2 text-sm placeholder:text-gray-400"
          type="text"
          placeholder="Add your new todo"
        />
        <Button
          @click="addTodo"
          class="bg-[#9149e9] h-9 w-12 flex items-center justify-center hover:cursor-pointer"
        >
          <AkPlus class="w-5 h-5 text-white" />
        </Button>
      </div>
      <ul v-for="(todo, index) in todos" :key="index" class="space-y-3">
        <div class="flex">
          <li
            @click="toggleShowDeleteButton(index)"
            class="font-medium text-xl w-full py-1 px-2 bg-[#f3f1f4] rounded-xl cursor-pointer break-words"
          >
            {{ todo.data }} 
          </li>
          <div
            v-if="todo.status"
            @click="handleClickTodo(index)"
            :class="{'scale-100': todo.status}"
            class="bg-red-700 w-[50px] flex justify-center items-center rounded-xl scale-0 transition-transform duration-300 cursor-pointer"
          >
            <AnFilledDelete class="text-white text-2xl" />
          </div>
        </div>
      </ul>
      <div class="mt-5 flex flex-col space-y-1 md:flex-col lg:flex-row items-center justify-between">
        <span class="sm:text-[18px]"
          >You have {{ todos.length }} pending tasks</span
        >
        <Button @click="clearAllTodo" class="bg-[#9149e9] text-white p-2 rounded-xl cursor-pointer">
          Clear All
        </Button>
      </div>
    </div>
  </div>
</template>

<style>
.bg-gradient {
  background: linear-gradient(to bottom, #a0eacb, #4b63e6);
}
</style>
