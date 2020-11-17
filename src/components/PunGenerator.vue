<template>
  <div>
    <h1>Random Pun Generator</h1>
    <span class="pun" id="selectedPun" type="text">{{ pun }}</span>

    <button class="copy-button" v-on:click="copyPun">Copy</button>
    <br />
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
  copy = new Vue({
    data: {
      el: "#selectedPun",
      message: ""
      // copyText: document.getElementById("selectedPun")?.innerHTML,
    },
    methods: {
      randomPun: function() {
        // TODO: Add puns
      },
      copyPun: function() {
        if (this.el) {
          const inputCopy = document.createElement("input");
          inputCopy.value = this.el;
          document.body.appendChild(inputCopy);
          inputCopy.select();
          inputCopy.setSelectionRange(0, 99999); // mobile
          document.execCommand("copy");
          document.body.removeChild(inputCopy);
          console.log(inputCopy);
        }
      }
    }
  });
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
