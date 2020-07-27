<template>
  <div id="app">
    <h1>Cat Component:</h1>
    <Cat />
    <h1>Dog Component:</h1>
    <Dog />
    <!-- <img
      alt="Vue logo"
      src="./assets/logo.png"
    > -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";
import Cat from "./components/1/Cat.vue";
import Dog from "./components/1/Dog.vue";
@Component({
  components: {
    HelloWorld,
    Dog,
    Cat
  }
})
export default class App extends Vue {
  created() {
    console.log("App created");
    console.log("this.$store App", this.$store);
  }
  mounted() {
    console.log("App mounted");
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
