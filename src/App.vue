<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Blockly
      id="blockly-editor"
      toolbox-href="/toolbox.xml"
      :options="{
        scrollbars: false,
        grid: {
          spacing: 30,
          length: 2,
          snap: true
        }
      }"
      v-on:blockly-change="onChange"
    />
  </div>
</template>

<script>
import Blockly from "./components/Blockly.vue";

export default {
  name: "app",
  components: {
    Blockly
  },
  methods: {
    onChange: function(event, workspace) {
      console.log(event.type, workspace);
    }
  }
};
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

#blockly-editor {
  height: 600px;
}
</style>
