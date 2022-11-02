<template>
  <div class="block p-3 max-w-sm border border-gray-200 shadow-md m-4 rounded-lg" :class="{'bg-gray-300': value.completed}">
    <div class="mx-2 flex flex-col justify-between h-full">
      <!--  Title  -->
      <div class="flex flex-row flex-wrap justify-between">
        <div class="text-lg font-semibold leading-relaxed underline">{{ value.title }}</div>
        <CheckCircleIcon class="w-6 text-green-700 hover:text-green-800" v-if="value.completed"></CheckCircleIcon>
        <XCircleIcon class="w-6 text-red-700 hover:text-red-800"  v-else></XCircleIcon>
      </div>
      <!--  Description  -->
      <div class="mt-2 flex-1 text-base font-light leading-2">
        {{ value.description }}
      </div>
      <!--  Completed  -->
      <div class="mt-3 flex justify-between">
        <InlineButton @click="markOpposite" :class="{'bg-green-700 hover:bg-green-800': !value.completed, 'bg-red-700 hover:bg-red-800': value.completed}">
          {{ value.completed ? 'Mark as incomplete' : 'Mark as Complete' }}
        </InlineButton>
        <RemoveButton @click="$emit('remove')"></RemoveButton>
      </div>
    </div>
  </div>
</template>

<script>

import InlineButton from "@/components/InlineButton.vue";
import { CheckCircleIcon, XCircleIcon } from "@heroicons/vue/24/solid";
import RemoveButton from "@/components/RemoveButton.vue";

export default {
  name: "ToDoListItem",
  components: {RemoveButton, InlineButton, CheckCircleIcon, XCircleIcon},
  props: {
    value: {
      type: Object,
      default: null
    }
  },
  methods: {
    markOpposite() {
      this.value.completed = !this.value.completed;
    }
  }
}


</script>

<style scoped>

</style>