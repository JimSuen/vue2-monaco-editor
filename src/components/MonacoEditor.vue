<template>
  <div id="editorContainer" class="contaier"></div>
</template>

<script>
import * as monaco from "monaco-editor";
export default {
  name: "MonacoEditor",
  props: {
    msg: String,
  },
  data() {
    return {
      count: 0,
      editor: null,
      LANGUAGE: "csharp",
    };
  },
  mounted() {
    const dom = document.getElementById("editorContainer");
    this.editor = monaco.editor.create(dom, {
      value: "// type your code \n",
      language: this.LANGUAGE,
      lineNumbers: "off",
      fontSize: "12",
      minimap: {
        enabled: false,
      },
    });
    monaco.languages.registerCompletionItemProvider(this.LANGUAGE, {
      provideCompletionItems() {
        // provideCompletionItems(model, position, token, context) {
        //   console.log("model", model.fileName);
        //   console.log("position", position);
        //   console.log("token", token);
        //   console.log("context", context);
        return {
          suggestions: [
            {
              label: "public",
              kind: monaco.languages.CompletionItemKind["Function"],
              insertText: "public",
              detail: "公共方法关键字",
            },
            {
              label: "private",
              kind: monaco.languages.CompletionItemKind["Function"],
              insertText: "private",
              detail: "私有方法关键字",
            },
            {
              label: "using",
              kind: monaco.languages.CompletionItemKind["Keyword"],
              insertText: "using",
              detail: "",
            },
            {
              label: "system",
              kind: monaco.languages.CompletionItemKind["module"],
              insertText: "system",
              detail: "",
            },
          ],
        };
      },
      resolveCompletionItem() {
        return null;
      },
      triggerCharacters: ["public", "private"],
    });
  },
};
</script>
<style scoped>
.contaier {
  width: 95%;
  height: 100%;
  min-height: 800px;
  height: 20px;
  border: 1px solid #ebeef5;
  text-align: left;
}
</style>
