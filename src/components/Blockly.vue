<template>
  <div class="blockly-editor">
    <div class="blockly-area" ref="area"></div>
    <xml class="blockly-toolbox" ref="toolbox" style="display:none">
      <slot></slot>
    </xml>
  </div>
</template>

<script>
import Blockly from "blockly";

export default {
  name: "Blockly",
  data() {
    return {
      workspace: null
    };
  },
  mounted() {
    this.workspace = Blockly.inject(this.$refs.area, {
      toolbox: this.$refs.toolbox
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.blockly-editor {
  position: relative;
  min-height: 300px;
}

.blockly-area {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>