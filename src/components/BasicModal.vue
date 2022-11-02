<template>
  <div v-show="value" tabindex="-1" class="overflow-y-auto overflow-x-hidden fixed inset-0 w-full h-screen flex items-center justify-center backdrop-blur-md backdrop-opacity-90">
    <div class="relative p-4 w-full max-w-2xl h-full md:h-auto">
      <div class="relative bg-white rounded-lg shadow border">
        <div class="flex justify-between items-start p-4 rounded-t border-b bg-gray-00">
          <h3 class="text-xl font-semibold text-gray-900">
            {{ title }}
          </h3>
          <InlineButton class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900" @click="close">
            <XMarkIcon class="w-4"></XMarkIcon>
          </InlineButton>
        </div>
        <div class="p-6 space-y-6">
          <slot>
            Content slot
          </slot>
        </div>

        <div v-if="showFooter" class="flex items-center p-6 space-x-2 rounded-b border-t border-gray-200">
          <slot name="footer"></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import InlineButton from "@/components/InlineButton.vue";
import {XMarkIcon} from "@heroicons/vue/24/solid";

export default {
  name: "BasicModal",
  components: {InlineButton, XMarkIcon},
  props: {
    value: {
      type: Boolean,
      default: true
    },
    showFooter: Boolean,
    title: String,
  },
  methods: {
    close() {
      this.$emit('input', false);
      this.$emit('close');
    }
  }
}
</script>

<style scoped>

</style>