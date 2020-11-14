<template>
  <div>
    <h1>Random Pun Generator</h1>
    <!-- TODO: Add pun into UI -->
    <span class="pun">{{ pun }}</span
    ><br />
    <button class="random-button" onclick="randomPun()">Randomize</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class PunGenerator extends Vue {
  @Prop() private msg!: string;
  public pun = "I knew a woman who owned a taser. Man, was she stunning!";
  randomPun = function() {
    // TODO: Add puns
  };
}
</script>

<style scoped>
.pun {
  width: 100%;
  justify-content: center;
  font-size: 35px;
}
.random-button {
  margin: 40px;
}
</style>
