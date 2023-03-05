<script setup>
import { ref } from "vue";
import { RouterLink } from "vue-router";
import { v4 as uuidV4 } from "uuid";

const todoInput = ref("");
const rememberInput = ref(false);

const todoList = ref(
  localStorage.TODOLIST ? JSON.parse(localStorage.TODOLIST) : []
);

const handleSubmit = () => {
  if (!todoInput.value) return;
  const newTodoList = [
    {
      id: uuidV4(),
      todo: todoInput.value,
      remember: rememberInput.value,
      createdAt: new Date(),
    },
    ...todoList.value,
  ];

  localStorage.setItem("TODOLIST", JSON.stringify(newTodoList));
  todoList.value = newTodoList;

  todoInput.value = "";
  rememberInput.value = false;
};

const deleteTodo = (id) => {
  const newTodoList = todoList.value.filter((todo) => todo.id !== id);

  localStorage.setItem("TODOLIST", JSON.stringify(newTodoList));
  todoList.value = newTodoList;
};
</script>

<template>
  <nav
    class="flex justify-between items-center bg-indigo-400 text-white px-4 py-2 shadow container w-full max-w-md mx-auto"
  >
    <a href="#" class="text-xl font-semibold leading-tight p-1">Vue Todo</a>
    <ul class="flex gap-x-4">
      <li>
        <RouterLink to="/" class="hover:text-gray-300 transition duration-300">
          Home
        </RouterLink>
      </li>
      <li>
        <RouterLink
          to="/about"
          class="hover:text-gray-300 transition duration-300"
        >
          About
        </RouterLink>
      </li>
    </ul>
  </nav>

  <main class="container w-full max-w-md mx-auto mt-8">
    <div class="flex flex-col gap-8">
      <form class="flex flex-col gap-2" @submit.prevent="handleSubmit">
        <input
          type="text"
          class="px-4 py-2 bg-gray-100 rounded shadow border-indigo-300 border-2 focus:outline-indigo-500"
          placeholder="What do you want to do?"
          autocomplete="off"
          v-model="todoInput"
          autofocus
        />
        <div class="flex gap-2">
          <input type="checkbox" id="remember" v-model="rememberInput" />
          <label for="remember">Remember Me</label>
        </div>
        <button
          class="px-3 py-2 bg-indigo-500 rounded text-white font-semibold text-sm uppercase hover:shadow focus:ring-4 focus:ring-indigo-500/20 transition duration-300"
          type="submit"
        >
          Save
        </button>
      </form>

      <section class="todolist">
        <h2
          class="text-xl font-semibold leading-tight border-b border-gray-500/50"
        >
          Your Todo List
        </h2>
        <ul class="max-h-[69vh] overflow-y-auto">
          <li
            class="w-full flex justify-between items-center"
            v-for="(todo, i) in todoList"
            :key="i"
          >
            <div>
              <p>
                <span
                  class="font-semibold text-sm font-mono"
                  :class="{
                    'text-red-500': todo.remember,
                    'text-lime-500': !todo.remember,
                  }"
                  >></span
                >
                {{ todo.todo }}
              </p>
              <span class="text-sm text-gray-500">{{
                new Date(todo.createdAt).toLocaleString()
              }}</span>
            </div>
            <button
              @click="deleteTodo(todo.id)"
              type="button"
              class="rounded-full border-indigo-500 border px-2"
            >
              X
            </button>
          </li>
        </ul>
      </section>
    </div>
  </main>
</template>
