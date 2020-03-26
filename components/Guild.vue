<template>
  <div v-if="data">
    <p>{{ data.name }} [{{ data.tag }}]</p>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  props: {
    guildId: String
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
    guildDetails() {
      axios
        .get(
          `https://cors-anywhere.herokuapp.com/https://api.guildwars2.com/v2/guild/${this.guildId}`
        )
        .then((res) => {
          this.data = res.status === 200 ? res.data : null
        })
    }
  }
}
</script>
