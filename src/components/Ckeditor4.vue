<template>
  <ckeditor
    v-model="editorData"
    :config="editorConfig"
    @ready="onEditorReady"
    @focus="onEditorFocus"
    @blur="onEditorBlur"
    @input="onEditorInput"
    @fileUploadRequest="onFileUploadRequest"
    @fileUploadResponse="onFileUploadResponse"
  />
</template>

<script>
import CKEditor from "@/utils/ckeditor4-vue";

export default {
  name: "Ckeditor4",
  data() {
    return {
      editorData: "<p>Content of the editor.</p>",
      editorConfig: {
        extraPlugins: "uploadimage",
        filebrowserUploadUrl: "http://localhost:8079/upload",
        removeButtons:
          "Subscript,Superscript,Styles,About,Blockquote,RemoveFormat,Source,Maximize,HorizontalRule,SpecialChar,Anchor,Scayt,Undo,Cut,Copy,Redo,Paste,PasteText,PasteFromWord",
        removeDialogTabs:
          "image:Link;image:advanced;link:target;link:upload;link:advanced",
        toolbarGroups: [
          { name: "clipboard", groups: ["clipboard", "undo"] },
          {
            name: "editing",
            groups: ["find", "selection", "spellchecker", "editing"]
          },
          { name: "styles", groups: ["styles"] },
          { name: "basicstyles", groups: ["basicstyles", "cleanup"] },
          { name: "forms", groups: ["forms"] },
          { name: "tools", groups: ["tools"] },
          { name: "document", groups: ["mode", "document", "doctools"] },
          { name: "others", groups: ["others"] },
          {
            name: "paragraph",
            groups: ["list", "indent", "blocks", "align", "bidi", "paragraph"]
          },
          { name: "links", groups: ["links"] },
          { name: "insert", groups: ["insert"] },
          { name: "colors", groups: ["colors"] },
          { name: "about", groups: ["about"] }
        ],
        imageUploadUrl: "http://localhost:8079/upload" // Adding drag and drop image upload.
      }
    };
  },
  components: {
    ckeditor: CKEditor.component
  },
  methods: {
    onEditorReady(evt) {
      console.log("Editor is ready.", { evt });
    },
    onEditorFocus(evt) {
      console.log("Editor focused.", { evt });
    },
    onEditorBlur(evt) {
      console.log("Editor blurred.", { evt });
    },
    onEditorInput(evt) {
      console.log("Editor data input.", { evt });
    },
    onFileUploadRequest(evt) {
      console.log("File Upload.", { evt });
    },
    onFileUploadResponse(evt) {
      console.log("File Uploaded.", { evt });
      evt.stop();

      // Get XHR and response.
      let data = evt.data;
      const xhr = data.fileLoader.xhr;
      const response = xhr.responseText.split("|");
      const temp1 = JSON.parse(response);

      if (!temp1.success) {
        // An error occurred during upload.
        data.message = temp1.msg;
        evt.cancel();
      } else {
        data.url = temp1.data.url;
      }
    }
  }
};
</script>