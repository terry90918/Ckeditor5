<template>
  <ckeditor
    v-model="editorData"
    :editor="editor"
    :config="editorConfig"
    @ready="onEditorReady"
    @focus="onEditorFocus"
    @blur="onEditorBlur"
    @input="onEditorInput"
    @destroy="onEditorDestroy"
  />
</template>

<script>
import CKEditor from '@ckeditor/ckeditor5-vue'

// ⚠️ NOTE: We don't use @ckeditor/ckeditor5-build-classic any more!
// Since we're building CKEditor from source, we use the source version of ClassicEditor.
import ClassicEditor from '@ckeditor/ckeditor5-editor-classic/src/classiceditor';

import EssentialsPlugin from '@ckeditor/ckeditor5-essentials/src/essentials';
import BoldPlugin from '@ckeditor/ckeditor5-basic-styles/src/bold';
import HeadingPlugin from '@ckeditor/ckeditor5-heading/src/heading';
import ItalicPlugin from '@ckeditor/ckeditor5-basic-styles/src/italic';
import LinkPlugin from '@ckeditor/ckeditor5-link/src/link';
import ParagraphPlugin from '@ckeditor/ckeditor5-paragraph/src/paragraph';

export default {
  name: 'Ckeditor5',
  data () {
    return {
      editor: ClassicEditor,
      editorData: '<p>Content of the editor.</p>',
      editorConfig: {
        plugins: [
          BoldPlugin,
          EssentialsPlugin,
          HeadingPlugin,
          ItalicPlugin,
          LinkPlugin,
          ParagraphPlugin
        ],
        toolbar: {
          items: ['heading', 'bold', 'italic', 'link', 'undo', 'redo']
        },
        language: 'en'
      }
    }
  },
  components: {
    ckeditor: CKEditor.component
  },
  methods: {
    onEditorReady( editor ) {
      console.log( 'Editor is ready.', { editor } );
    },
    onEditorFocus( event, editor ) {
      console.log( 'Editor focused.', { event, editor } );
    },
    onEditorBlur( event, editor ) {
      console.log( 'Editor blurred.', { event, editor } );
    },
    onEditorInput( data, event, editor ) {
      console.log( 'Editor data input.', { event, editor, data } );
    },
    onEditorDestroy( editor ) {
      console.log( 'Editor destroyed.', { editor } );
    }
  }
}
</script>