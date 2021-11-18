<template>
  <section class="min-w-screen min-h-screen py-6 bg-gray-100 dark:bg-gray-800">
    <app-title />
    <main-wrapper>
      <transition
        enter-active-class="duration-500 ease"
        leave-active-class="opacity-0 duration-500 ease"
        enter-class="opacity-0"
      >
        <nuxt keep-alive />
      </transition>
    </main-wrapper>
  </section>
</template>

<script>
import AppTitle from '@/components/AppTitle'
import MainWrapper from '@/components/MainWrapper'

export default {
  components: {
    MainWrapper,
    AppTitle,
  },
}
</script>
