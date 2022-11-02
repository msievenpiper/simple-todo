<template>
  <BasicModal :value="showModal" title="Create new ToDo" @close="close" show-footer>
    <form @submit.prevent="save">
      <div class="grid gap-6 mb-6 md:grid-cols-1">
        <div>
          <label for="title" class="block mb-2 text-sm font-medium text-gray-900">Title</label>
          <input v-model="item.title" type="text" id="title" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" required>
        </div>
        <div>
          <label for="description" class="block mb-2 text-sm font-medium text-gray-900">Description</label>
          <textarea v-model="item.description" id="description" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"></textarea>
        </div>
      </div>
    </form>
    <template #footer>
      <InlineButton @click="save" class="bg-blue-400 rounded-full">
        Save
      </InlineButton>
    </template>
  </BasicModal>
</template>

<script>
import BasicModal from "@/components/BasicModal.vue";
import InlineButton from "@/components/InlineButton.vue";

export default {
  name: "NewItemModal",
  components: {InlineButton, BasicModal},
  data() {
    return {
      showModal: false,
      item: null
    };
  },
  methods: {
    reset() {
      this.item = {
        title: '',
        description: '',
      };
    },
    show() {
      this.showModal = true;
    },
    close() {
      this.reset();
      this.showModal = false;
    },
    save() {
      this.$emit('created', this.item);
      this.close();
    }
  },
  beforeMount() {
    this.reset();
  }
}
</script>

<style scoped>

</style>