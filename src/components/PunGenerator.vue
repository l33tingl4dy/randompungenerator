<template>
  <div>
    <h1>Random Pun Generator</h1>
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
  public puns = [
    "I knew a woman who owned a taser. Man, was she stunning!",
    "I lost my job at the bank on my very first day. A woman asked me to check her balance, so I pushed her over",
    "It's hard to explain puns to kleptomaniacs because they always take things literally",
    "Two windmills are standing in a wind farm. One asks, “What’s your favorite kind of music?” The other says, “I’m a big metal fan.”"
  ];
  public pun = this.puns[Math.floor(Math.random() * this.puns.length)];
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
  padding: 10%;
}
.random-button {
  margin: 40px;
}
</style>
