<template>
  <!-- Loading UI -->
  <div v-if="loading" class="section">
    <p class="title">Loading Diff</p>
    <p class="subtitle">Diff ID: {{ diffID }}</p>
  </div>

  <div v-else class="columns is-multiline is-vcentered mx-3">
    <div class="column is-full">
      <!-- @todo Move this out to somewhere -->
      <p class="title">View diff</p>

      <!-- @todo Make this bigger and more obvious -->
      <p class="subtitle">{{ file.name }}</p>
    </div>

    <!-- @todo Use a editor library instead to do things like show line number and all -->

    <div class="column is-half">
      <textarea
        :value="file.content"
        class="textarea has-fixed-size"
        disabled
      ></textarea>
    </div>

    <div class="column is-half">
      <textarea class="textarea has-fixed-size"></textarea>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface File {
  name: string;
  content: string;
}

export default defineComponent({
  name: "ViewDiff",

  props: {
    // @todo Error if no string passed in
    diffID: {
      type: String,
      required: true,
    },
  },

  data(): { loading: boolean; file: File } {
    return {
      // View starts off as loading
      loading: true,

      file: {
        name: "HomeView.js",
        content: "some random text",
      },
    };
  },

  created() {
    // Load original file the moment component is created
    this.getOriginal();
  },

  methods: {
    /** Get original file from API */
    async getOriginal() {
      // this.loading = false;
      // this.file = res.file
      // this.diffID

      setTimeout(() => {
        this.loading = false;
      }, 2000);
    },
  },
});
</script>

<style scoped>
textarea {
  height: 100vh;
}
</style>
