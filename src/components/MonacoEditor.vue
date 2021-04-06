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
      minimap: {
        enabled: false,
      },
    });
    monaco.languages.registerCompletionItemProvider(this.LANGUAGE, {
      provideCompletionItems() {
        return {
          suggestions: [
            {
              label: "public", // 显示的提示内容
              kind: monaco.languages.CompletionItemKind["Function"], // 用来显示提示内容后的不同的图标
              insertText: "public", // 选择后粘贴到编辑器中的文字
              detail: "公共方法关键字", // 提示内容后的说明
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
  border: 1px solid #ebeef5;
  text-align: left;
}
</style>
