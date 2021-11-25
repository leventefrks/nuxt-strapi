<template lang="html">
  <div class="flex flex-wrap justify-center gap-6">
    <div
      v-for="menu in menus"
      :key="menu.id"
      class="shadow-md transform hover:-translate-y-1 duration-200"
    >
      <div
        class="relative bg-gray-50 rounded-tl-md rounded-tr-md overflow-hidden"
      >
        <button
          class="
            absolute
            top-2
            right-2
            text-red-500
            cursor-pointer
            focus:outline-none focus:ring-2
            rounded
            focus:ring-green-500 focus:border-transparent
          "
        >
          <heart-icon size="25" />
        </button>
        <figure>
          <img
            :src="`http://localhost:1337${menu.image.url}`"
            :alt="menu.mealName"
            quality="20"
            class="w-full object-cover h-40"
          />
        </figure>
      </div>
      <div class="bg-gray-50 dark:bg-gray-700 shadow-lg rounded-lg -mt-4 w-64">
        <div class="flex flex-col items-start p-5">
          <h2 class="font-bold text-gray-700 dark:text-gray-50 text-md">
            {{ menu.mealName }}
          </h2>
          <nuxt-link
            :to="{ name: 'slug', params: { slug: menu.path, id: menu.id } }"
            class="
              inline-flex
              items-center
              text-green-500
              hover:text-green-400
              font-bold
              text-sm
              rounded
              duration-200
              focus:outline-none
              focus:ring-2
              focus:ring-green-500
              focus:border-transparent
            "
            >More info
            <chevron-right-icon class="text-gray-400" size="15" />
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ChevronRightIcon, HeartIcon } from 'vue-feather-icons'

export default {
  components: {
    ChevronRightIcon,
    HeartIcon,
  },

  props: {
    menus: {
      type: Array,
      default: () => [],
    },
  },
}
</script>
