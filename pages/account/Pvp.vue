<template>
  <div v-if="stats">
    <div class="d-flex">
      <h1 class="mr-auto">PvP stats</h1>
      <h3 class="p-2">
        Rank {{ stats.pvp_rank }} x{{ stats.pvp_rank_rollovers }}
      </h3>
    </div>
    <p>Rank points total: {{ stats.pvp_rank_points }}</p>
    <div class="d-flex">
      <h3 class="p-2">Total Wins: {{ stats.aggregate.wins }}</h3>
      <h3 class="p-2">Total Losses: {{ stats.aggregate.losses }}</h3>
      <h3 class="p-2">Win ratio: {{ totalRatio }}%</h3>
    </div>
    <div
      v-for="[profesion, data] in Object.entries(stats.professions)"
      :key="profesion"
    >
      {{ profesion }}: {{ data }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      accountAPI: null,
      stats: null
    }
  },
  computed: {
    total() {
      return this.stats.aggregate.wins + this.stats.aggregate.losses
    },
    totalRatio() {
      return ((this.stats.aggregate.wins * 100) / this.total).toFixed(2)
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
          console.log(this.stats)
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
