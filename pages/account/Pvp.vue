<template>
  <div v-if="stats">
    <div class="d-flex">
      <h1 class="mr-auto">PvP stats</h1>
      <h3 class="p-2">
        Rank {{ stats.pvp_rank }} x{{ stats.pvp_rank_rollovers }}
      </h3>
    </div>
    <p>Rank points total: {{ stats.pvp_rank_points }}</p>
    <Ratio :wins="stats.aggregate.wins" :losses="stats.aggregate.losses" />
    <div
      v-for="[profession, data] in Object.entries(stats.professions)"
      :key="profession"
      class="shadow p-3 mb-5 bg-white rounded"
    >
      <PvPprofession :data="data" :index="profession" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import PvPprofession from '~/components/PvPprofession.vue'
import Ratio from '~/components/Ratio.vue'
export default {
  components: {
    PvPprofession,
    Ratio
  },
  data() {
    return {
      accountAPI: null,
      stats: null
    }
  },
  methods: {
    pvpAccountStats() {
      axios
        .get(
          `https://cors-anywhere.herokuapp.com/https://api.guildwars2.com/v2/pvp/stats`,
          {
            headers: {
              Authorization: `Bearer ${this.accountAPI}`
            }
          }
        )
        .then((res) => {
          this.stats = res.status === 200 ? res.data : null
        })
    }
  },
  mounted() {
    if (localStorage.API) {
      this.accountAPI = localStorage.API
    } else {
      window.location.href = '/'
    }
    this.pvpAccountStats()
  }
}
</script>
