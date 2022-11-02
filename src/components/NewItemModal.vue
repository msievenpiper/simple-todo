<template>
  <BasicModal :value="showModal" title="Create new ToDo" @close="close" show-footer>
    <form @submit.prevent="save">
      <div class="grid gap-6 mb-6 md:grid-cols-1">
        <div>
          <BasicTextField ref="title" v-model="item.title" label="Title" required></BasicTextField>
        </div>
        <div>
          <BasicTextField area ref="description" v-model="item.description"></BasicTextField>
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
import BasicTextField from "@/components/BasicTextField.vue";

export default {
  name: "NewItemModal",
  components: {BasicTextField, InlineButton, BasicModal},
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
    validate() {
      if (this.item.title == '') {
        this.$refs.title.errors("Title is required");
        return false;
      }
      return true;
    },
    save() {
      if (this.validate()) {
        this.$emit('created', this.item);
        this.close();
      }
    }
  },
  beforeMount() {
    this.reset();
  }
}
</script>

<style scoped>

</style>