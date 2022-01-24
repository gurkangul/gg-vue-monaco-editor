# gg-vue-monaco-editor

> [Monaco Editor](https://github.com/Microsoft/monaco-editor) for Vue.

Demo: https://happy-dubinsky-0b4f38.netlify.app/

## Installation

```bash
npm install --save gg-vue-monaco-editor
```

## Usage

### Vue JS

```js
// vue.config.js
const MonacoWebpackPlugin = require("monaco-editor-webpack-plugin");

module.exports = {
  configureWebpack: {
    plugins: [new MonacoWebpackPlugin()],
  },
};
```

```js
<template>
    <MonacoEditor
      :options="options"
      @change="onChange"
      customClass="myClass"
      customStyle="height:500px"
    ></MonacoEditor>
</template>

<script>
import MonacoEditor from 'gg-vue-monaco-editor'
export default {
  name: "App",
  components: {
    MonacoEditor
  },
  data() {
    return {
      options:{
            value: `function test(){
    console.log("test")
   }`,
          language: "javascript",
          fontSize: "13px",
          theme: "vs-dark",
          roundedSelection: false,
          scrollBeyondLastLine: false,
        };
    }
  },
  methods: {
    onChange(value) {
      console.log(value);
    }
  }
};
</script>
```

### Nuxt JS

> touch ./plugins/editor.js

```js
// editor.js
import Vue from "vue";
import MonacoEditor from "gg-vue-monaco-editor";

Vue.component("MonacoEditor", MonacoEditor);
```

```js
// nuxt.config.js
const MonacoWebpackPlugin = require("monaco-editor-webpack-plugin");

module.exports = {
  // ...

  plugins: [{ src: "~plugins/editor", mode: "client" }],

  build: {
    // ...
    plugins: [new MonacoWebpackPlugin()],
  },
};
```

```js
<template>
  <client-only>
    <MonacoEditor
      :options="options"
      @onChange="onChange"
      customClass="myClass"
      customStyle="height:500px"
    ></MonacoEditor>
  </client-only>
</template>

<script>
export default {
  data() {
    return {
      options: {
        value: `function test(){
    console.log("test")
}`,
        language: 'javascript',
        fontSize: '13px',
        automaticLayout: true,
        theme: 'vs-dark',
        roundedSelection: false,
        scrollBeyondLastLine: false,
      },
    }
  },
  methods: {
    onChange(value) {
      console.log(value)
    },
  },
}
</script>



```

## Properties

| Property    | Description                                                                                                         |
| ----------- | ------------------------------------------------------------------------------------------------------------------- |
| options     | Use orginal monaco-editor options.You can find the other options in here https://microsoft.github.io/monaco-editor/ |
| customStyle | you can use css (Example= height:500px)                                                                             |
| customClass | if you want use your global class                                                                                   |

## Events

| Event    | Description                     |
| -------- | ------------------------------- |
| onChange | Emits the value on every change |

## License

This project is licensed under the MIT License
