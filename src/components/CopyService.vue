<template>
  <div id="copyJoke">
    <p>Some joke</p>
  </div>
</template>
<script lang="ts">
import { Vue } from "vue-property-decorator";
export default class CopyService extends Vue {}

CopyService.component("", {
  data: {
    message: "pun"
  },
  //   computed: {
  //     copiedPun: function (): {
  //       return "happy punning" + document.getElementById("selectedPun");
  //     },
  //   },
  methods: {
    doCopy: function() {
      this.$copyText(this.message).then(
        function(e) {
          alert("Copied");
          console.log(e);
        },
        function(e) {
          alert("Can not copy");
          console.log(e);
        }
      );
    }
  }
});
</script>

<style scoped></style>
