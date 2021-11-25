<template lang="html">
  <section class="w-full">
    <div
      class="
        max-w-3xl
        mx-auto
        mt-8
        shadow-xl
        bg-gray-50
        dark:bg-gray-700
        rounded-md
      "
    >
      <div class="p-5">
        <h2 class="mb-4 font-bold text-gray-500 dark:text-gray-50 text-3xl">
          {{ menu.mealName }}
        </h2>
        <figure>
          <img
            :src="`http://localhost:1337${menu.image.url}`"
            :alt="menu.mealName"
            class="w-full object-cover h-72"
          />
        </figure>
        <h3 class="font-bold text-gray-500 dark:text-gray-50 text-md">
          Ingredients
        </h3>
        <div class="dark:text-gray-50">{{ menu.ingredients }}</div>
        <div class="flex items-center justify-between">
          <badge :is-gluten-free="glutenFree" />
          <div class="text-2xl text-red-600 font-bold">$ {{ menu.price }}</div>
        </div>
        <nuxt-link
          to="/"
          class="
            inline-flex
            items-center
            gap-x-1
            text-green-500
            hover:text-green-400
            font-bold
            text-xs
          "
        >
          <chevron-left-icon class="text-gray-400" size="15" />
          Go Back
        </nuxt-link>
      </div>
    </div>
  </section>
</template>

<script>
import { ChevronLeftIcon } from 'vue-feather-icons'
import Badge from '@/components/Badge'
import GetMenu from '@/apollo/queries/menu'

export default {
  components: {
    ChevronLeftIcon,
    Badge,
  },

  async asyncData({ app, params, query }) {
    const client = app.apolloProvider.defaultClient

    const result = await client.query({
      query: GetMenu,
      variables: {
        id: query.id,
      },
    })

    const menu = result.data.menu
    return {
      menu,
    }
  },
}
</script>
