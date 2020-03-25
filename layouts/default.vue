<template>
  <div class="layout row">
    <header class="header col-sm-2">
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
    </header>
    <div class="container-fluid col-sm-8 shadow p-3 mb-5 bg-white rounded">
      <nuxt />
    </div>
  </div>
</template>

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
  position: absolute;
  align-items: center;
}
.container {
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
</style>
