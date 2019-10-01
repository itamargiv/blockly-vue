<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Blockly id="blockly-editor">
      <block type="controls_if"></block>
      <block type="controls_repeat_ext"></block>
      <block type="logic_compare"></block>
      <block type="math_number"></block>
      <block type="math_arithmetic"></block>
      <block type="text"></block>
      <block type="text_print"></block>
    </Blockly>
  </div>
</template>

<script>
import Blockly from "./components/Blockly.vue";

export default {
  name: "app",
  components: {
    Blockly
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
