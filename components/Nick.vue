<template>
  <div class="nick">
    <p>
      {{ name }}
      <img v-if="commander" src="../data/commander.png" class="commander" />
    </p>
  </div>
</template>
<script>
export default {
  props: {
    name: {
      type: String,
      default: ''
    },
    commander: {
      type: Boolean,
      default: false
    }
  }
}
</script>
<style>
.nick {
  display: flex;
  font-size: 3em;
  margin-bottom: 3%;
}
.commander {
  width: 8%;
  margin-left: 20px;
}
</style>
