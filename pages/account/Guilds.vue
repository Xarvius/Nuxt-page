<template>
  <div>
    <div v-if="chosedGuild">
      <p @click="chosedGuild = null">Back to list</p>
      <h1>Guild</h1>
      <GuildDetails />
    </div>

    <div v-else>
      <h1>Guilds</h1>
      <div
        v-for="(guild, index) in guilds"
        :key="index"
        class="shadow p-3 mb-5 bg-white rounded"
      >
        <Guild :guild-id="guild" :index="index" />
      </div>
    </div>
  </div>
</template>

<script>
import Guild from '~/components/Guild.vue'
import GuildDetails from '~/components/GuildDetails.vue'
export default {
  components: {
    Guild,
    GuildDetails
  },
  data() {
    return {
      guilds: [],
      chosedGuild: null
    }
  },
  mounted() {
    if (localStorage.guilds) {
      this.guilds = localStorage.guilds.split(',')
    } else {
      window.location.href = '/'
    }
  }
}
</script>
<style scoped>
.mb-5 {
  margin-bottom: 1.6rem !important;
}
</style>
