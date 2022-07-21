<template>
  <div class="mx-3">
    <div v-for="(line, i) in prettyHtml" :key="i">
      <span v-if="line.charAt(0) === '+'" class="has-background-success">
        {{ line }}
      </span>
      <span v-else-if="line.charAt(0) === '-'" class="has-background-danger">
        {{ line }}
      </span>
      <span v-else>
        {{ line }}
      </span>
    </div>

    <hr />
    <hr />
    <hr />

    <div v-for="(line, i) in prettyHtml" :key="i">
      {{ line }}
    </div>
  </div>
</template>

<script lang="ts">
import * as Diff from "diff";

export default {
  data() {
    return {
      oldString: "old string",
      newString: "new string",
    };
  },

  computed: {
    diff() {
      return Diff.createPatch(
        "fileName",
        this.oldString,
        this.newString,
        // "oldHeader",

        // Header names should be the same to show it as changed rather than renamed
        "newHeader",
        "newHeader",

        // Passing in -1 to show all unchanged lines
        { context: -1 }
      );
    },

    prettyHtml() {
      //   console.log(this.diff.split("\n"));
      //   return this.diff;
      return this.diff.split("\n");
    },
  },
};
</script>

<style>
.d2h-code-line-ctn {
  user-select: none;
}
</style>
