<template>
  <div v-if="guild">
    <div class="d-flex">
      <h4 class="mr-auto">{{ guild.name }} [{{ guild.tag }}]</h4>

      <div class="p-2">Level {{ guild.level }}/69</div>
      <div
        :aria-controls="`collapse-${index}`"
        :aria-expanded="visible ? 'true' : 'false'"
        @click="visible = !visible"
        class="m-1"
      >
        <b-icon-chevron-down v-if="!visible" />
        <b-icon-chevron-up v-else />
      </div>
    </div>
    <b-collapse :id="`collapse-${index}`" v-model="visible">
      <div class="d-flex">
        <div class="mr-auto">MOTD</div>
        <div class="p-2">
          <b-icon-person-fill />
          {{ guild.member_count }} / {{ guild.member_capacity }}
        </div>
      </div>
      <b-card>{{ guild.motd }}</b-card>
      <div class="wallet d-flex flex-row">
        <div class="p-2">
          <img src="../data/Aetherium.png" class="icon" alt="Aetherium" />
          {{ guild.aetherium }}
        </div>
        <div class="p-2">
          <img src="../data/Favor.png" class="icon" alt="Favor" />
          {{ guild.favor }}
        </div>
      </div>
    </b-collapse>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  props: {
    guildId: {
      type: String,
      default: null
    },
    index: {
      type: Number,
      default: null
    }
  },
  data() {
    return {
      guild: null,
      accountAPI: null,
      visible: false
    }
  },
  mounted() {
    this.accountAPI = localStorage.API ? localStorage.API : null
    if (this.accountAPI) this.guildDetails()
  },
  methods: {
    guildDetails() {
      axios
        .get(
          `https://cors-anywhere.herokuapp.com/https://api.guildwars2.com/v2/guild/${this.guildId}`,
          {
            headers: {
              Authorization: `Bearer ${this.accountAPI}`
            }
          }
        )
        .then((res) => {
          this.guild = res.status === 200 ? res.data : null
          console.log(this.guild)
        })
    }
  }
}
</script>
<style scoped>
.icon {
  height: 40px;
}
</style>
