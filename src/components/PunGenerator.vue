<template>
  <div>
    <h1>Random Pun Generator</h1>
    <span class="pun" id="selectedPun" type="text">{{ joke }}</span>

    <button class="copy-button" v-on:click="copyPun">Copy</button>
    <br />
    <button class="random-button" v-on:click="getJoke">Randomize</button>
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

  // JokeAPI
  joke = new Vue({
    data: {
      baseUrl: "https://sv443.net/jokeapi/v2",
      categories: [
        "Programming",
        "Miscellaneous",
        "Pun",
        "Spooky",
        "Christmas"
      ],
      params: ["blacklistFlags=nsfw,religious,racist", "idRange=0-100"],
      xhr: new XMLHttpRequest(),
      joke: ""
    },
    methods: {
      getJoke: function() {
        this.xhr.open(
          "GET",
          this.baseUrl +
            "/joke/" +
            this.categories.join(",") +
            "?" +
            this.params.join("&")
        );
        this.xhr.onreadystatechange;
        if (this.xhr.readyState == 4 && this.xhr.status < 300) {
          const randomJoke = JSON.parse(this.xhr.responseText);
          if (randomJoke.type == "single") {
            alert(randomJoke.joke);
            this.joke = randomJoke.joke;
          } else {
            alert(randomJoke.setup);
            alert(randomJoke.delivery);
            this.joke = randomJoke.setup + randomJoke.delivery;
          }
        } else if (this.xhr.readyState == 4) {
          alert(
            "Error while requesting joke.\n\nStatus code: " +
              this.xhr.status +
              "\nServer response: " +
              this.xhr.responseText
          );
        }
        this.xhr.send();
        return this.joke;
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
