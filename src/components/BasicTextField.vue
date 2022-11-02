<template>
  <div class="mb-2">
    <label for="input" class="block mb-2 text-sm font-medium ">{{ label }}</label>
    <input v-model="value" v-if="!area" type="text" id="input" :class="inputClass" class="border text-sm rounded-lg block w-full p-2.5" :placeholder="placeholder" v-bind="$attrs">
    <textarea v-model="value" v-if="area" id="input" :class="inputClass" class="border text-sm rounded-lg block w-full p-2.5" :placeholder="placeholder" v-bind="$attrs"></textarea>
    <p v-if="message != ''" :class="messageClass" class="mt-2 text-sm">{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "BasicTextField",
  props: {
    value: {},
    area: Boolean,
    label: String,
    placeholder: String,
  },
  data(){
    return {
      success: false,
      error: false,
      message: '',
    };
  },
  computed: {
    inputClass() {
      if (this.success) {
        return 'text-green-700 bg-green-50 border-green-500 text-green-900 placeholder-green-700 focus:ring-green-500 focus:border-green-500';
      }
      if (this.error) {
        return 'text-red-700 bg-red-50 border-red-500 text-red-900 placeholder-red-700 focus:ring-red-500 focus:border-red-500';
      }
      return 'border-blue-500 placeholder-blue-700 focus:ring-blue-500 focus:border-blue-500';
    },
    messageClass() {
      if (this.success) {
        return 'text-green-600';
      }
      if (this.error) {
        return 'text-red-600';
      }
      return 'text-gray-600';
    },
  },
  methods: {
    reset() {
      this.success = false;
      this.error = false;
      this.message = '';
    },
    errors(message) {
      this.success = false;
      this.error = true;
      this.setMessage(message);
    },
    setMessage(message) {
      this.message = message;
      setTimeout(() => {
        this.reset();
      }, 3000);
    }
  }
}
</script>

<style scoped>

</style>