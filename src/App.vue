<template>
  <div id="app">
    <div class="d-flex vh-100 justify-content-center align-items-center">
      <div class="w-25">
        <div class="m-2 p-2 rounded border">
            {{ content }}
        </div>
        <form class="p-2" action="#">
          <textarea v-model="content" class="form-control" name="content">
          </textarea>
          <button @click.prevent="save" class="btn btn-success mt-2" type="submit">Save</button>
        </form>
      </div>
    </div>
    <div class="border bg-info w-100 pt-2 px-4">
      <pre class="text-light">{{ payload }}</pre>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      content: 'Some Content',
      payload: {
        content: null
      }
    }
  },
  methods: {
    save() {
      this.payload.content = this.content
    }
  }
}
</script>

<style>
</style>
