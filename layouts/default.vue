<template>
  <div class="layout row">
    <header class="header col-sm-2">
      <div
        v-show="width"
        aria-controls="menu"
        :aria-expanded="visible ? 'true' : 'false'"
        class="nav-item border nav__link h1"
        @click="visible = !visible"
      >
        <b-icon-list />
      </div>
      <b-collapse id="menu" v-model="visible">
        <ul class="nav flex-column h1">
          <NLink class="nav__link" to="/">
            <li class="nav-item border text-dark">
              <b-icon-house />
            </li>
          </NLink>
          <NLink class="nav__link" to="/Account/">
            <li class="nav-item border text-dark">
              <b-icon-person />
            </li>
          </NLink>
        </ul>
      </b-collapse>
    </header>
    <div
      class="container-fluid col-sm-8 shadow p-3 mb-5 bg-white rounded overflow-auto"
    >
      <nuxt />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      width: true,
      visible: true
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize)
    this.visible = screen.width > 575
    this.handleResize()
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    handleResize() {
      this.width = window.innerWidth < 575
      this.visible = window.innerWidth > 575
    }
  }
}
</script>

<style>
body {
  font-family: -apple-system, system-ui, BlinkMacSystemFont, 'Segoe UI', Roboto,
    'Helvetica Neue', Arial, sans-serif;
  margin: 0;
  padding: 0;
  line-height: 1.5;
}

.layout {
  margin: 0 auto;
  background-image: url('https://d3b4yo2b5lbfy.cloudfront.net/wp-content/uploads/wallpapers/GuildWars2_NornBonusWP02-1920x1200.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  position: fixed;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
}

.header {
  align-items: center;
}
.container-fluid {
  height: 97%;
  margin-top: 1%;
}
.nav__link {
  margin-top: 10%;
  background-color: white;
  box-shadow: 0 0 5px black;
}
.nav-item {
  padding-left: 42%;
  transition: box-shadow 0.3s;
}
.nav-item:hover {
  box-shadow: 0 0 15px;
}
@media (max-width: 576px) {
  .container-fluid {
    overflow-y: visible;
    max-height: 88%;
  }
  .nav__link {
    margin-top: 3%;
    margin-bottom: 2%;
  }
}
</style>
