<template>
  <div>
    <div class="apiForm">
      <ApiForm v-if="!data" @form-send="formSend" />
      <p v-else @click="data = null">Change</p>
    </div>
    <div v-if="data" class="panel">
      <Nick :name="data.name" :commander="data.commander" />
      <BasicAccountInfo />
      <Category />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Category from '~/components/Category.vue'
import Nick from '~/components/Nick.vue'
import ApiForm from '~/components/ApiForm.vue'
import BasicAccountInfo from '~/components/BasicAccountInfo.vue'

export default {
  components: {
    Category,
    Nick,
    ApiForm,
    BasicAccountInfo
  },
  data() {
    return {
      data: {
        name: null,
        commander: null
      }
    }
  },
  mounted() {
    if (localStorage.API && localStorage.name && localStorage.commander) {
      this.data.name = localStorage.name
      this.data.commander = localStorage.commander === 'true'
    }
  },
  methods: {
    formSend(apiKey) {
      axios
        .get(
          'https://cors-anywhere.herokuapp.com/https://api.guildwars2.com/v2/account',
          {
            headers: {
              Authorization: `Bearer ${apiKey}`
            }
          }
        )
        .then((res) => {
          this.data = res.status === 200 ? res.data : null
          localStorage.API = apiKey
          localStorage.name = res.data.name
          localStorage.commander = res.data.commander
          localStorage.guilds = res.data.guilds
        })
    }
  }
}
</script>

<style>
.panel {
  padding: 1%;
}

.apiForm {
  position: absolute;
  right: 1%;
}
</style>
