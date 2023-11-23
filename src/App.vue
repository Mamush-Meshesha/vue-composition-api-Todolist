<script setup>
import { ref } from "vue";
const newTodo = ref("");
const defaultData = [
  {
    done: false,
    content: "Write a blog Post",
  },
];

const todosData = JSON.parse(localStorage.getItem("todos")) || defaultData;

const todos = ref(todosData);

const addTodo = () => {
  if (newTodo.value) {
    todos.value.push({
      done: false,
      content: newTodo.value,
    });
    newTodo.value = "";
  }
  saveDate();
};
const doneTodo = (todo) => {
  todo.done = !todo.done;
  saveDate();
};
const removeTodo = (index) => {
  todos.value.splice(index, 1);
  saveDate();
};

const saveData = () => {
  const storageData = JSON.stringify(todos.value);
  localStorage.setItem("todos", storageData);
};
</script>

<template>
  <div class="bg-[#0f0245]">
    <div class="container mx-auto w-screen h-screen pt-20">
      <div class="text-white font-bold text-4xl flex justify-center">
        <h1>Todo App</h1>
      </div>
      <div>
        <form action="" @submit.prevent="addTodo">
          <div class="flex flex-col">
            <label for="newTodo" class="text-white text-2xl font-bold"
              >New Todos</label
            >
            <input
              v-model="newTodo"
              type="text"
              name="newTodo"
              id=""
              autocomplete="on"
              class="h-12 rounded-md border outline-none bg-transparent px-3 text-white"
            />
            <button class="bg-[#696e7a] h-12 my-5 rounded-r-md">
              Add Todo
            </button>
          </div>
        </form>
      </div>
      <div class="text-white">
        <h1 class="text-4xl font-bold justify-center flex">Todo list</h1>
        <hr class="text-8xl font-bold border-x-4 my-2" />
        <div class="py-6">
          <ul>
            <div>
              <li
                v-for="(todo, index) in todos"
                :key="index"
                class="border h-12 rounded flex justify-between"
              >
                <div
                  class="ml-[20px] flex items-center"
                  :class="{ done: todo.done }"
                  @click="doneTodo(todo)"
                >
                  <span class="">
                    {{ todo.content }}
                  </span>
                </div>
                <button
                  @click="removeTodo(index)"
                  class="mr-[50px] bg-[#696e7a] h-8 mt-2 w-20 rounded-md"
                >
                  Remove
                </button>
              </li>
            </div>
          </ul>
          <h1 v-if="todos.length === 0">Empity list</h1>
        </div>
      </div>
    </div>
  </div>
</template>
