<template>
  <div class="w-full mx-auto lg:w-5/6 rounded-md">
    <div class="bg-white shadow-md rounded my-6">
      <table class="min-w-max w-full table-auto">
        <thead>
          <tr
            class="
              bg-gray-200
              dark:bg-gray-700 dark:text-gray-200
              text-gray-600 text-xs
              md:text-sm
              leading-normal
              tracking-wider
            "
          >
            <th class="p-2 text-center">Meal Name</th>
            <th class="hidden md:flex p-2 text-center">Gluten free</th>
            <th class="p-2 text-center">Info</th>
          </tr>
        </thead>
        <tbody class="text-white text-sm">
          <tr
            v-for="menu in menus"
            :key="menu.id"
            class="
              border-b
              text-gray-400
              dark:border-gray-600 dark:hover:bg-gray-800
              hover:text-gray-100 hover:bg-gray-300
              dark:bg-gray-700
            "
          >
            <td class="p-2 text-left">
              <div class="flex items-center">
                <div class="mr-2">
                  <img
                    class="w-6 h-6 rounded-full"
                    :src="`http://localhost:1337${menu.image.url}`"
                  />
                </div>
                <span class="cursor-default">{{ menu.mealName }}</span>
              </div>
            </td>
            <td class="hidden md:flex p-2 text-center cursor-default">
              <badge :is-gluten-free="menu.glutenFree" />
            </td>
            <td class="p-2 text-center">
              <nuxt-link
                :to="{
                  name: 'slug',
                  params: {
                    slug: menu.path,
                  },
                }"
                class="
                  inline-flex
                  items-center
                  text-green-500
                  hover:text-green-400
                  duration-200
                  font-bold
                  focus:outline-none focus:ring-2 focus:ring-green-500
                  rounded-md
                  text-xs
                  focus:border-transparent
                "
                >More Info
                <chevron-right-icon class="text-gray-400" size="15" />
              </nuxt-link>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { ChevronRightIcon } from 'vue-feather-icons'
import Badge from '@/components/Badge'

export default {
  components: {
    ChevronRightIcon,
    Badge,
  },

  props: {
    menus: {
      type: Array,
      default: () => [],
    },
  },
}
</script>
