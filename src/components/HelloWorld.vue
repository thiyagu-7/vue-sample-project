<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,
      <br>check out the
      <a
        href="https://cli.vuejs.org"
        target="_blank"
        rel="noopener"
      >vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel"
          target="_blank"
          rel="noopener"
        >babel</a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint"
          target="_blank"
          rel="noopener"
        >eslint</a>
      </li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li>
        <a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a>
      </li>
      <li>
        <a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a>
      </li>
      <li>
        <a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a>
      </li>
      <li>
        <a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a>
      </li>
      <li>
        <a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a>
      </li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li>
        <a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a>
      </li>
      <li>
        <a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-devtools#vue-devtools"
          target="_blank"
          rel="noopener"
        >vue-devtools</a>
      </li>
      <li>
        <a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a>
      </li>
      <li>
        <a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a>
      </li>
    </ul>
    <div>
      Preloaded value - {{preLoad}}
      <br>
    </div>
    <br>
    <div>
      <button v-on:click="getData">Fetch dynamic data</button>
      <br>
      Dynamic data - {{info}}
      <br>
    </div>
    <div>
      Backend app data - {{backendAppPreLoad}}
      <br>
    </div>
    <div>
      Backend dynamic interaction <br>
      <input v-model="inputData"/>
      <button v-on:click="processRequest(inputData)">Fetch data</button>
      {{backendResponse}}
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      preLoad: "Should not be shown",
      info: "Initial value",
      backendAppPreLoad: "Should not be shown..",
      backendResponse: "Init value",
      inputData:"" //without this it issues a warning
    };
  },
  methods: {
    getData() {
      console.log("Called");
      axios
        .get("https://api.coindesk.com/v1/bpi/currentprice.json")
        .then(response => (this.info = response));
    },
    processRequest(input) {
      console.log("Calling backend with input " + input);
       axios
        .get("https://hidden-dusk-89678.herokuapp.com/hello/" + input)
        .then(response => (this.backendResponse = response));
    }
  },
  mounted() {
    axios
      .get("https://api.coindesk.com/v1/bpi/historical/close.json")
      .then(response => (this.preLoad = response));

    axios
      .get("https://hidden-dusk-89678.herokuapp.com/get") 
      .then(response => (this.backendAppPreLoad = response))
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
