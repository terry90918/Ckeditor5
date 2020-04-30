<template>
  <ckeditor
    v-model="editorData"
    :config="editorConfig"
    @ready="onEditorReady"
    @focus="onEditorFocus"
    @blur="onEditorBlur"
    @input="onEditorInput"
  />
</template>

<script>
import CKEditor from 'ckeditor4-vue'

export default {
  name: 'Ckeditor4',
  data () {
    return {
      editorData: '<p>Content of the editor.</p>',
      editorConfig: {
        extraPlugins: 'uploadimage',
        filebrowserUploadUrl: 'http://localhost:8081/upload',
        removeButtons: 'Subscript,Superscript,Styles,About,Blockquote,RemoveFormat,Source,Maximize,HorizontalRule,SpecialChar,Anchor,Scayt,Undo,Cut,Copy,Redo,Paste,PasteText,PasteFromWord',
        removeDialogTabs: 'image:Link;image:advanced;link:target;link:upload;link:advanced',
        toolbarGroups: [
          { name: 'clipboard', groups: [ 'clipboard', 'undo' ] },
          { name: 'editing', groups: [ 'find', 'selection', 'spellchecker', 'editing' ] },
          { name: 'styles', groups: [ 'styles' ] },
          { name: 'basicstyles', groups: [ 'basicstyles', 'cleanup' ] },
          { name: 'forms', groups: [ 'forms' ] },
          { name: 'tools', groups: [ 'tools' ] },
          { name: 'document', groups: [ 'mode', 'document', 'doctools' ] },
          { name: 'others', groups: [ 'others' ] },
          { name: 'paragraph', groups: [ 'list', 'indent', 'blocks', 'align', 'bidi', 'paragraph' ] },
          { name: 'links', groups: [ 'links' ] },
          { name: 'insert', groups: [ 'insert' ] },
          { name: 'colors', groups: [ 'colors' ] },
          { name: 'about', groups: [ 'about' ] }
        ],
        // uploadUrl: '/apps/ckfinder/3.4.5/core/connector/php/connector.php?command=QuickUpload&type=Files&responseType=json',
      }
    }
  },
  components: {
    ckeditor: CKEditor.component
  },
  methods: {
    onEditorReady(evt) {
      console.log('Editor is ready.', { evt })
    },
    onEditorFocus(evt) {
      console.log('Editor focused.', { evt })
    },
    onEditorBlur(evt) {
      console.log('Editor blurred.', { evt })
    },
    onEditorInput(evt ) {
      console.log('Editor data input.', { evt })
    }
  }
}
</script>