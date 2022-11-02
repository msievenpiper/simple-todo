<template>
  <form @submit.prevent="$emit('search')">
    <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-gray-300">Search</label>
    <div class="relative">
      <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
        <MagnifyingGlassCircleIcon class="w-6 text-grey-400 hover:text-grey-800"></MagnifyingGlassCircleIcon>
      </div>
      <input v-model="value" type="search" id="default-search"
             class="block p-4 pl-10 w-full text-sm rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500"
             placeholder="Search ToDo's">
    </div>
  </form>
</template>

<script>

import {MagnifyingGlassCircleIcon} from "@heroicons/vue/24/solid";

export default {
  name: "DefaultSearchBar",
  components: {MagnifyingGlassCircleIcon},
  props: {
    value: String
  }
}
</script>

<style scoped>

</style>