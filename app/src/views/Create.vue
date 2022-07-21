<template>
  <div class="columns is-multiline is-vcentered mx-3">
    <div class="column">
      <p class="title">Create a new diff</p>
    </div>

    <div class="column is-narrow">
      <button class="button is-light is-success" @click="create">Create</button>
    </div>

    <!-- @todo Add input element to upload file directly instead -->

    <div class="column is-full">
      <label>
        <b>Enter an optional file name</b>

        <input
          v-model="fileName"
          type="text"
          class="input"
          placeholder="File Name"
        />
      </label>
    </div>

    <div class="column is-full">
      <!-- @todo Use a editor library instead to do things like show line number and all -->
      <textarea
        class="textarea has-fixed-size"
        placeholder="Enter your code here"
      ></textarea>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Create",

  data(): { fileName: string } {
    return { fileName: "" };
  },

  methods: {
    async create() {
      this.fileName;

      // Call API
      // If filename is blank, generate a random file name??

      // Once created, redirect back to home view
      this.$router.push({ name: "home" });
    },
  },
});
</script>

<style scoped>
textarea {
  height: 100vh;
}
</style>
