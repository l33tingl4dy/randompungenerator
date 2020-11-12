<template>
  <div>
    <h1>Random Pun Generator</h1>
    <!-- TODO: Add pun into UI -->
    <button onclick="randomPun()">Randomize</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class PunGenerator extends Vue {
  @Prop() private msg!: string;
}

const randomPun = function() {
  // TODO: Add puns
  const pun1 = "I knew a woman who owned a taser. Man, was she stunning!";
  return pun1;
};
</script>

<style scoped></style>
