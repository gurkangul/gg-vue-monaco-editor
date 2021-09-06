<template>
  <div ref="code-editor" :class="customClass" :style="customStyle" />
</template>

<script>
import * as monaco from "monaco-editor/esm/vs/editor/editor.api";

export default {
  name: "MonacoEditor",
  props: {
    customStyle: { type: String, default: "" },
    customClass: { type: String, default: "m-editor" },
    options: {
      type: Object,
      default: () => {
        return {
          value: `
function test() {
  console.log("test")
}`,
          language: "javascript",
          fontSize: "13px",
          automaticLayout: true,
          theme: "vs-dark",
          roundedSelection: false,
          scrollBeyondLastLine: false,
        };
      },
    },
  },
  data() {
    return {
      editor: {},
    };
  },
  methods: {
    _onChange() {
      this.editor.getModel().onDidChangeContent((event) => {
        this.$emit("onChange", { ...event, value: this.editor.getValue() });
      });
    },
  },
  mounted() {
    this.editor = monaco.editor.create(this.$refs["code-editor"], this.options);
    this._onChange();
    // this.$refs["code-editor"].style.height =
    //   this.editor.getModel().getLineCount() * 20 + "px";
  },
  beforeDestroy() {
    this.editor && this.editor.dispose();
  },
};
</script>

<style scoped>
.m-editor {
  height: 300px;
}
</style>

