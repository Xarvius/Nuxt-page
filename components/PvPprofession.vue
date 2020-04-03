<template>
  <div v-if="index">
    <div class="d-flex">
      <h4 class="mr-auto">{{ firstCapital }}</h4>
      <div
        :aria-controls="`collapse-${index}`"
        :aria-expanded="visible ? 'true' : 'false'"
        class="m-1"
        @click="visible = !visible"
      >
        <b-icon-chevron-down v-if="!visible" />
        <b-icon-chevron-up v-else />
      </div>
    </div>
    <b-collapse :id="`collapse-${index}`" v-model="visible">
      <b-card>
        <Ratio :wins="data.wins" :losses="data.losses" />
        <div class="d-flex" v-if="wins && losses">
          <h3 class="p-2">Desertions: {{ data.desertions }}</h3>
          <h3 class="p-2">Byes: {{ data.byes }}</h3>
          <h3 class="p-2">Forfeits: {{ data.forfeits }}</h3>
        </div>
      </b-card>
    </b-collapse>
  </div>
</template>
<script>
import Ratio from '~/components/Ratio.vue'
export default {
  components: {
    Ratio
  },
  props: {
    data: {
      type: Object,
      default: null
    },
    index: {
      type: String,
      default: null
    }
  },
  data() {
    return {
      visible: false
    }
  },
  computed: {
    firstCapital() {
      return this.index.charAt(0).toUpperCase() + this.index.slice(1)
    }
  }
}
</script>
