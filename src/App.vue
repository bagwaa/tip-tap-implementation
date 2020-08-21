<template>
  <div id="app">
    <div class="d-flex vh-100 justify-content-center align-items-center">
      <div class="w-25">
        <form class="p-2" action="#">
          <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
            <div class="menubar">
              <button class="mb-2 mr-2 btn btn-light border" :class="{ 'is-active': isActive.bold() }" @click.prevent="commands.bold">
                B
              </button>
              <button class="mb-2 mr-2 btn btn-light border" :class="{ 'is-active': isActive.heading({ level: 2 }) }" @click.prevent="commands.heading({ level: 2 })">
                  H2
              </button>
              <button class="mb-2 mr-2 btn btn-light border" :class="{ 'is-active': isActive.heading({ level: 3 }) }" @click.prevent="commands.heading({ level: 3 })">
                  H3
              </button>
              <button class="mb-2 mr-2 btn btn-light border" :class="{ 'is-active': isActive.bullet_list() }" @click.prevent="commands.bullet_list">
                  <svg xmlns="http://www.w3.org/2000/svg" style="width: 15px; height: 15px;" viewBox="0 0 20 20"><path d="M1 4h2v2H1V4zm4 0h14v2H5V4zM1 9h2v2H1V9zm4 0h14v2H5V9zm-4 5h2v2H1v-2zm4 0h14v2H5v-2z"/></svg>
              </button>
              <button class="mb-2 btn btn-light border" @click.prevent="showImagePrompt(commands.image)">
                  <svg xmlns="http://www.w3.org/2000/svg" style="width: 15px; height: 15px;" viewBox="0 0 20 20"><path d="M0 4c0-1.1.9-2 2-2h16a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V4zm11 9l-3-3-6 6h16l-5-5-2 2zm4-4a2 2 0 1 0 0-4 2 2 0 0 0 0 4z"/></svg>
              </button>
            </div>
          </editor-menu-bar>
          <editor-content class="border rounded" :editor="editor" />
        </form>
        <div class="m-2 p-2 h-4">
            {{ content }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import { Heading, Bold, ListItem, BulletList, Image } from 'tiptap-extensions'

export default {
  name: 'App',
  components: {
    EditorContent,
    EditorMenuBar
  },
  data() {
    return {
      editor: new Editor({
        content: '',
        extensions: [
          new Bold(),
          new Heading(),
          new BulletList(),
          new ListItem(),
          new Image()
        ],
        onUpdate: ({ getHTML }) => {
          this.content = getHTML()
        },
      }),
      content: '',
    }
  },
  methods: {
    showImagePrompt(command) {
        const src = prompt('Enter the url of your image here')
        if (src !== null) {
            command({ src })
        }
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  },
}
</script>

<style>
  .is-active {
    background: lightgray;
  }
  .ProseMirror {
    height: 100%;
    padding: 10px 10px;
  }
</style>
