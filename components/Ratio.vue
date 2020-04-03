<template>
  <div class="d-flex" v-if="wins && losses">
    <h3 class="p-2">Total Wins: {{ wins }}</h3>
    <h3 class="p-2">Total Losses: {{ losses }}</h3>
    <h3 class="p-2">Win ratio: {{ totalRatio }}%</h3>
  </div>
</template>
<script>
export default {
  props: {
    wins: {
      type: Number,
      default: null
    },
    losses: {
      type: Number,
      default: null
    }
  },
  computed: {
    total() {
      return this.wins + this.losses
    },
    totalRatio() {
      return ((this.wins * 100) / this.total).toFixed(2)
    }
  }
}
</script>
