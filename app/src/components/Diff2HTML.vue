<template>
  <div class="mx-3">
    <div v-html="htmlOutput"></div>
  </div>
</template>

<script lang="ts">
import * as Diff2Html from "diff2html";
import "diff2html/bundles/css/diff2html.min.css";

import * as Diff from "diff";

export default {
  data() {
    return {
      oldString: "old string",
      newString: `new string`,
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

    htmlOutput() {
      return Diff2Html.html(this.diff, {
        // Dont show file names as there will only be 1 file being compared
        // The UI will be created manually by the app instead of using this library
        drawFileList: false,

        // @todo Add select for this
        matching: "none",
        // matching: "lines",
        // matching: "words",

        // @todo Add toggle for this
        outputFormat: "side-by-side",
        // outputFormat: "line-by-line",
      });
    },
  },
};
</script>

<style>
.d2h-code-line-ctn {
  user-select: none;
}
</style>
