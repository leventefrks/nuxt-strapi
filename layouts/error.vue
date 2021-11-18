<template lang="html">
  <section
    class="
      min-w-screen min-h-screen
      flex flex-col
      items-center
      justify-center
      space-y-4
    "
  >
    <h1 class="text-center dark:text-white text-green-500 font-bold text-5xl">
      {{ error.statusCode === 404 ? 'Page not found' : 'An error occurred' }}
    </h1>
    <nuxt-link to="/" class="dark:text-white text-green-500 text-xl"
      >Home page</nuxt-link
    >
  </section>
</template>

<script>
export default {
  props: {
    error: {
      type: Object,
      default: () => ({}),
    },
  },
}
</script>
