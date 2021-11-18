<template lang="html">
  <div class="relative w-full flex flex-col">
    <aside
      class="
        absolute
        left-0
        top-0
        md:flex
        hidden
        flex-col
        items-center
        space-y-4
        p-4
        bg-gray-50
        dark:bg-gray-700
        rounded-md
        shadow-lg
      "
    >
      <button
        class="
          p-1
          rounded-md
          text-gray-500
          dark:text-gray-50
          hover:text-gray-300
          duration-200
          focus:outline-none
          focus:ring-2
          focus:ring-green-500
          focus:border-transparent
        "
        aria-label="Ascending Order"
        @click="onAscendedSort"
      >
        <trending-up-icon size="20" />
      </button>
      <button
        class="
          p-1
          text-gray-500
          rounded-md
          dark:text-gray-50
          duration-200
          hover:text-gray-300
          focus:outline-none
          focus:ring-2
          focus:ring-green-500
          focus:border-transparent
        "
        aria-label="Descending Order"
        @click="onDescendedSort"
      >
        <trending-down-icon size="20" />
      </button>
      <button
        class="
          p-1
          text-gray-500
          rounded-md
          dark:text-gray-50
          duration-200
          hover:text-gray-300
          focus:outline-none
          focus:ring-2
          focus:ring-green-500
          focus:border-transparent
        "
        aria-label="List View"
        @click="onListView"
      >
        <menu-icon size="20" />
      </button>
      <button
        class="
          p-1
          text-gray-500
          rounded-md
          dark:text-gray-50
          duration-200
          hover:text-gray-300
          focus:outline-none
          focus:ring-2
          focus:ring-green-500
          focus:border-transparent
        "
        aria-label="Grid View"
        @click="onGridView"
      >
        <more-horizontal-icon size="25" />
      </button>
    </aside>
    <div class="max-w-5xl flex items-center justify-center space-x-4 mb-6">
      <div
        class="
          flex
          items-center
          space-y-4
          md:space-y-0 md:space-x-8
          py-4
          px-6
          bg-gray-50
          rounded-md
          shadow-xl
          dark:bg-gray-700
        "
      >
        <div
          class="
            flex
            items-center
            bg-gray-100
            dark:bg-gray-600
            p-2
            w-72
            space-x-3
            rounded-lg
          "
        >
          <button v-if="searchValue" aria-label="Reset Search" @click="onReset">
            <x-icon
              aria-label="Delete Search"
              class="text-gray-500 dark:text-gray-50 cursor-pointer"
              size="20"
            />
          </button>
          <search-icon v-else class="text-gray-300 flex-shrink-0" size="20" />
          <input
            v-model.trim="searchValue"
            class="
              w-full
              p-1
              bg-gray-100
              rounded-md
              dark:bg-gray-600 dark:text-gray-50
              focus:outline-none
              focus:ring-2
              focus:ring-green-500
              focus:border-transparent
            "
            type="text"
            placeholder="Menu name or keyword..."
          />
          <transition
            name="fade"
            enter-active-class="duration-300 ease"
            leave-active-class="opacity-0 duration-300 ease"
            enter-class="opacity-0"
          >
          </transition>
        </div>
      </div>
    </div>
    <div class="max-w-5xl">
      <card v-if="isGridViewVisible" :menus="filteredMenus" />
      <list v-else :menus="filteredMenus" />
    </div>
  </div>
</template>

<script>
import {
  MoreHorizontalIcon,
  TrendingDownIcon,
  TrendingUpIcon,
  SearchIcon,
  MenuIcon,
  XIcon,
} from 'vue-feather-icons'
import Card from '@/components/Card'
import List from '@/components/List'
import Menus from '@/apollo/queries/menus'

export default {
  components: {
    MoreHorizontalIcon,
    TrendingDownIcon,
    TrendingUpIcon,
    SearchIcon,
    MenuIcon,
    XIcon,
    Card,
    List,
  },

  apollo: {
    $loadingKey: 'loading',
  },

  async asyncData({ app, params }) {
    const client = app.apolloProvider.defaultClient

    const res = await client.query({
      query: Menus,
    })

    const { menus } = res.data
    return {
      menus,
    }
  },

  data() {
    return {
      menus: [],
      loading: 0,
      isAscendingOrder: true,
      isDescendingOrder: false,
      searchValue: '',
      isListViewVisible: false,
      isGridViewVisible: true,
    }
  },

  computed: {
    filteredMenus() {
      const recipes = this.menus

      if (this.searchValue) {
        return recipes.filter((menu) =>
          menu.mealName.toLowerCase().includes(this.searchValue.toLowerCase())
        )
      }

      if (this.isAscendingOrder) {
        return recipes.sort((a, b) => a.mealName.localeCompare(b.mealName))
      }

      if (this.isDescendingOrder) {
        return recipes.sort((a, b) => b.mealName.localeCompare(a.mealName))
      }

      return recipes
    },
  },

  methods: {
    onAscendedSort() {
      this.onReset()
      this.isAscendingOrder = true
      this.isDescendingOrder = false
    },

    onDescendedSort() {
      this.onReset()
      this.isDescendingOrder = true
      this.isAscendingOrder = false
    },

    onReset() {
      this.searchValue = ''
    },

    onListView() {
      this.isListViewVisible = true
      this.isGridViewVisible = false
    },

    onGridView() {
      this.isGridViewVisible = true
      this.isListViewVisible = false
    },
  },
}
</script>
