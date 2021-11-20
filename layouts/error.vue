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
    <page-title>{{
      error.statusCode === 404 ? 'Page not found' : 'An error occurred'
    }}</page-title>
    <nuxt-link
      to="/"
      class="
        flex
        items-center
        text-green-500
        hover:text-green-400
        text-sm
        font-bold
        rounded
        duration-200
        focus:outline-none
        focus:ring-2
        focus:ring-green-500
        focus:border-transparent
      "
    >
      <chevron-left-icon class="text-gray-400" size="15" />
      Go Back</nuxt-link
    >
  </section>
</template>

<script>
import { ChevronLeftIcon } from 'vue-feather-icons'
import PageTitle from '@/components/PageTitle'

export default {
  components: {
    ChevronLeftIcon,
    PageTitle,
  },

  props: {
    error: {
      type: Object,
      default: () => ({}),
    },
  },

  mounted() {
    console.log(this.$route.params)
  },
}
</script>
