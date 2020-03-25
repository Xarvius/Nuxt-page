<template>
  <div v-if="data">
    <p>{{ data.name }} [{{ data.tag }}]</p>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  props: {
    guildID: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      data: null
    }
  },
  mounted() {
    this.guildDetails()
  },
  methods: {
    guildDetails: async () => {
      try {
        await axios
          .get(
            `https://cors-anywhere.herokuapp.com/https://api.guildwars2.com/v2/guild/${this.guildID}`
          )
          .then((res) => {
            this.data = res.status === 200 ? res.data : null
          })
      } catch (error) {
        this.data = null
      }
    }
  }
}
</script>
