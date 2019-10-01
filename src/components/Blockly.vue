<template>
  <div class="blockly-editor">
    <div class="blockly-area" ref="area"></div>
  </div>
</template>

<script>
import Blockly from "blockly";

export default {
  name: "Blockly",
  props: {
    toolboxHref: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      workspace: null
    };
  },
  async mounted() {
    const toolbox = await fetch(this.toolboxHref).then(res => res.text());
    this.workspace = Blockly.inject(this.$refs.area, { toolbox });

    window.addEventListener("resize", this.resizeBlockly, false);

    this.resizeBlockly();
  },
  destroyed() {
    window.removeEventListener("resize", this.resizeBlockly, false);
  },
  methods: {
    resizeBlockly: function() {
      Blockly.svgResize(this.workspace);
    }
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