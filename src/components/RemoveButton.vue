<template>
  <InlineButton v-bind="$attrs">
      <TrashIcon class="w-6 text-red-700 hover:text-red-800"></TrashIcon>
  </InlineButton>
</template>

<script>

import InlineButton from "@/components/InlineButton.vue";
import {TrashIcon} from "@heroicons/vue/24/solid";

export default {
  name: "RemoveButton",
  components: {InlineButton, TrashIcon},
  inheritAttrs: true
}
</script>

<style scoped>

</style>