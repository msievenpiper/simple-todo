<template>
  <button v-bind="$attrs" type="button"
          class="text-white focus:ring-4 font-medium rounded-lg text-sm px-3 py-1.5 focus:outline-none">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "InlineButton",
  inheritAttrs: true
}
</script>

<style scoped>

</style>