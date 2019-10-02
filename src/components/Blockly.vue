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
    /**
     * URL to load toolbox configurations from. Must be a valid toolbox XML.
     * @see See [Blockly docs](https://developers.google.com/blockly/guides/configure/web/toolbox).
     */
    toolboxHref: {
      type: String,
      required: true
    },
    /**
     * Blockly configuration options.
     *
     * @see See [Blockly docs](https://developers.google.com/blockly/guides/get-started/web#configuration).
     */
    options: Object
  },
  data() {
    return {
      workspace: null
    };
  },
  async mounted() {
    const toolbox = await fetch(this.toolboxHref).then(res => res.text());
    this.workspace = Blockly.inject(this.$refs.area, {
      ...this.options,
      toolbox
    });

    this.workspace.addChangeListener(event => {
      /**
       * Triggeres whenever the Blockly workspace changes
       *
       * @type {object}
       *
       * @property {object} event The blockly event |||
       * @property {object} workspace The current active workspace |||
       * @property {object} Blockly The exposed Blockly namespace
       */
      this.$emit("blockly-change", event, this.workspace, Blockly);
    });

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

<docs>
### Features

- Fully Responsive
- Loads External toolbox configuration
- Exposes change event handler
- Implements Blockly options

### Examples

#### Basic Usage

```js
<Blockly toolbox-href="simple-toolbox.xml" />
```

#### Custom Height

```js
<Blockly toolbox-href="example-toolbox.xml" :style="{ height: '600px' }"/>
```

#### Handle Events

```js
function printCode(event, workspace, Blockly){
    const code = Blockly.JavaScript.workspaceToCode(workspace);

    document.getElementById('blockly-output').innerText = code;
}

<Blockly toolbox-href="simple-toolbox.xml" v-on:blockly-change="printCode"/>

<pre id="blockly-output" :style="{ 
  minHeight: '300px',
  padding: '1rem', 
  background: '#451f47',  
  color: '#fdfff0'}"></pre>
```

#### Complex Toolbox with Options

```js
<Blockly toolbox-href="/toolbox.xml"
  :options="{
    scrollbars: false,
    grid: {
      spacing: 30,
      length: 2,
      snap: true
    }
  }" />
```
</docs>