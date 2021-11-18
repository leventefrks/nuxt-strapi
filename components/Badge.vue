<template>
  <span
    :class="[
      ' text-white py-1 px-3 rounded-full text-xs',
      { 'bg-purple-500': isGlutenFree, 'bg-yellow-500': !isGlutenFree },
    ]"
    >{{ isGlutenFree ? 'Gluten Free' : 'Consists Gluten' }}
  </span>
</template>

<script>
export default {
  props: {
    isGlutenFree: {
      type: Boolean,
      default: false,
    },
  },
}
</script>
