<template>
  <div>
    <form class="form-inline" @submit="prevent(apiKey, $event)">
      <input v-model="apiKey" placeholder="edit me" class="form-control" />
      <input type="submit" value="Submit" class="btn btn-primary" />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      apiKey: null
      // C584E9F6-2244-744C-BD98-DCB4BB5CE24B49C0F240-282B-4798-AE81-E028DBD09346
    }
  },
  mounted() {
    if (localStorage.API) {
      this.apiKey = localStorage.API
    }
    if (!localStorage.name && this.apiKey) {
      this.sendApi(this.apiKey)
    }
  },
  methods: {
    prevent(api, event) {
      event.preventDefault()
      this.sendApi(api)
    },
    sendApi(api) {
      this.$emit('form-send', api)
    }
  }
}
</script>
