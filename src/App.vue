<template>
  <div id="app">
    <div id="nav">
      <b-navbar class="is-dark">
        <template #brand>
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                <img
                    src="https://media-cdn.tripadvisor.com/media/photo-s/07/ed/20/4d/getlstd-property-photo.jpg"
                    alt="Lightweight UI components for Vue.js based on Bulma"
                >
            </b-navbar-item>
        </template>
        <template #start>
            <b-navbar-item href="#">
                Home
            </b-navbar-item>
            <b-navbar-item href="#">
                Documentation
            </b-navbar-item>

        </template>


    </b-navbar>
      <!-- <router-link to="/">Home</router-link> | -->
      <!-- <router-link to="/about">About</router-link> -->
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}

#nav {
  // padding: 30px;

  a {
    font-weight: bold;
    color: white;

    &.router-link-exact-active {
      color: white;
    }
  }
}

.navbar{
  background:url(https://i.pinimg.com/originals/61/76/bb/6176bb6884a3594e2a816661d826b121.jpg);
  background-position: center;
  background-repeat: no-repeat;
  color:white;
  text-align:center;
}

.navbar-start a.navbar-item:hover{
  background:url(https://i.pinimg.com/originals/3b/94/66/3b9466a15339b766466ca212c4758372.jpg);
}

.navbar-link:not(.is-arrowless)::after{
  color:white;
}
</style>
