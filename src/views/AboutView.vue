<template>
  <main
    class="h-screen container w-full max-w-md mx-auto border-r border-l flex justify-center items-center flex-col"
  >
    <h1 class="text-lg font-semibold leading-tight text-gray-800">
      About This Page
    </h1>

    <p>
      This project is available on github! Check it out
      <a
        href="https://github.com/kevinnvm/vue-todo"
        class="text-blue-500 hover:text-indigo-500 transition duration-300"
        target="_blank"
        >Here</a
      >
    </p>
    <p>Fun fact: this project is finished under 15 minutes</p>
    <RouterLink
      to="/"
      class="text-blue-500 hover:text-indigo-500 transition duration-300"
      >Back to Home</RouterLink
    >
  </main>
</template>