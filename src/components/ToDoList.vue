<template>
  <div class="mx-auto px-2 mt-2">
    <!-- Search bar for items -->
    <div class="mx-auto w-2/3">
      <DefaultSearchBar v-model="search" @input="updateSearch"></DefaultSearchBar>
    </div>
    <!-- Let's create a list type view  -->
    <div v-if="displayList.length == 0">
      <div class="mx-auto mt-4 p-4 mb-4 text-sm text-green-700 bg-green-100 rounded-lg" >
        <span class="font-medium">Nothing ToDo!</span> Try adding some new items
      </div>
    </div>
    <div class="mt-4 flex flex-row flex-wrap justify-between mx-auto w-10/12">
      <ToDoListItem v-for="(item, key) in displayList"
                    @remove="removeItem(item.id)"
                    :key="key" class="max-w-[25%] min-w-[400px]"
                    :value="item">
      </ToDoListItem>
    </div>
    <!-- Buttons Row -->
    <div class="mt-4 mr-8 flex flex-row justify-end">
      <InlineButton @click="$refs.modal.show()" class="bg-blue-400 rounded-full">
        <PlusIcon class="w-8 text-white"></PlusIcon>
      </InlineButton>
    </div>

    <NewItemModal ref="modal" @created="handleNewItem"></NewItemModal>

  </div>
</template>

<script>

import ToDoListItem from "@/components/ToDoListItem.vue";
import InlineButton from "@/components/InlineButton.vue";
import { PlusIcon } from "@heroicons/vue/24/solid"
import NewItemModal from "@/components/NewItemModal.vue";
import DefaultSearchBar from "@/components/DefaultSearchBar.vue";

export default {
  name: "ToDoList",
  components: {DefaultSearchBar, NewItemModal, InlineButton, ToDoListItem, PlusIcon},
  data() {
    return {
      currentId: 1,
      list: [],
      displayList: [],
      search: ''
    };
  },
  methods: {
    handleNewItem(item) {
      this.addNewItem(item.title, item.description);
    },
    addNewItem(title, description) {
      this.list.push({
        id: this.currentId++,
        title: title,
        description: description,
        completed: false
      });
    },
    updateSearch(event) {
      this.search = event.target.value;
    },
    filterList() {
      if (this.search == null || this.search == '') {
        return this.list;
      }
      return this.list.filter(item => item.title.toLowerCase().includes(this.search.toLowerCase()))
    },
    sortList() {
      this.displayList = this.filterList().sort((a, b) => {
        return a.completed - b.completed; // Sort asc
      });
    },
    removeItem(id) {
      const index = this.list.findIndex(item => item.id == id);
      if (index != -1) {
        this.list.splice(index, 1);
      }
    },
    updateStorage() {
      window.localStorage.setItem('id', JSON.stringify(this.currentId));
      window.localStorage.setItem('list', JSON.stringify(this.list));
    }
  },
  mounted() {
    // Let's use the local storage
    if (this.list.length == 0) {
      // For the sake of an example let's create an add a set of items
      this.addNewItem('Create a todo app', 'Make a very simple front end application for the tutorial/portfolio');
      this.addNewItem('Make some items', 'Add at least one item to the list for the sake of a demo');
      this.addNewItem('Generate some interest', "Make sure it looks right otherwise it won't be very interesting");
    }
   },
  beforeMount() {
    const list = window.localStorage.getItem('list');
    const decoded = JSON.parse(list);
    if (list != null && Array.isArray(decoded)) {
      this.list = decoded;
      this.currentId = Number.parseInt(window.localStorage.getItem('id'))
    }
  },
  watch: {
    list: {
      deep: true,
      handler() {
        this.sortList();
        this.updateStorage();
      }
    },
    search() {
      this.sortList();
    }
  },
  beforeUnmount() {
    this.updateStorage();
  }
}

</script>

<style scoped>

</style>