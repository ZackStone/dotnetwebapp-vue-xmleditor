<template>
    <v-ace-editor
      class="xml-editor"
      ref="xmlEditor"
      :style="`height: ${height};`"
      :lang="'xml'"
      :theme="'chrome'"
      :options="options"
      :placeholder="'Enter XML content here...'"
      v-model:value="content" />
  </template>
  
<script>
import { VAceEditor } from 'vue3-ace-editor';
import ace from 'ace-builds';
import themeChromeUrl from 'ace-builds/src-noconflict/theme-chrome?url';
import modeXmlUrl from 'ace-builds/src-noconflict/mode-xml?url';

ace.config.setModuleUrl('ace/theme/chrome', themeChromeUrl);
ace.config.setModuleUrl('ace/mode/xml', modeXmlUrl);
  
export default {
  name: 'XmlEditor',
  components: {
    VAceEditor
  },
  props: ['modelValue', 'height'],
  emits: ['update:modelValue'],
  data() {
    return {
      content: this.modelValue,
      options: {
        useWorker: false,
        loadWorkerFromBlob: false,
      }
    };
  },
  watch: {
    modelValue(newValue) {
      this.content = newValue;
    },
    content(newValue) {
      this.$emit('update:modelValue', newValue);
    }
  }
}
</script>

<style>
.xml-editor {
  .ace_content > .ace_layer.ace_text-layer > .ace_line > span {
    font: 12px / normal 'Monaco', 'Menlo', 'Ubuntu Mono', 'Consolas', 'Source Code Pro', 'source-code-pro', monospace;
  }
}
</style>