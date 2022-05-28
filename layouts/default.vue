<template>
  <div class="header">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <ul class="navbar-nav mr-auto my-2 my-lg-0">
        <div class="wrapper">
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/resumen">Resumen</NuxtLink>
                </li>
            </div>
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/admins">Administratores</NuxtLink>
                </li>
            </div>
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/logs">Logs Servicios</NuxtLink>
                </li>
            </div>
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/logst">Logs Tareas</NuxtLink>
                </li>
            </div>
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/red">Red</NuxtLink>
                </li>
            </div>
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/configuracion">Configuración</NuxtLink>
                </li>
            </div>
            <!-- <div class="box3">
                <li>
                    <NuxtLink style="color:white" to="/login">Login</NuxtLink>
                </li>
            </div> -->
        </div>
      </ul>
            <form class="form-inline my-2 my-lg-0">
              <b-button type="button" class="btn btn-outline-success my-2 my-sm-0" v-on:click="setinfo" to="/login">
                <b-icon icon="power" style="color:white">
                </b-icon>
              </b-button>
            </form>
    </nav>
    <main>
      <Nuxt />
    </main>
  </div>
</template>
<script>
import axios from "axios";
export default {
    data: function () {
        return {};
    },
    components: {},
    methods: {
        async setinfo(){
          let adminenuso=localStorage.getItem("id");
          let resp = `http://127.0.0.1:8000/api/logout?id=${adminenuso}`;
          await axios.post(resp).then((data) => {
            // console.log(resp);
          });
          localStorage.removeItem('level');
          localStorage.removeItem('id');
        }
    },
    watch: {},
    mounted: function () {},
};
</script>
<style>
/* home route and active route will show in bold as it matches / and /about */
a.nuxt-link-active {
  font-weight: bold;
}
/* exact link will show the primary color for only the exact matching link */
a.nuxt-link-exact-active {
  color: #00c58e;
}

body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto,
    Helvetica Neue, Arial, Noto Sans, sans-serif, Apple Color Emoji,
    Segoe UI Emoji, Segoe UI Symbol, Noto Color Emoji;
  margin: 0;
}

main {
  margin: 0 auto;
  padding: 0 1rem;
  margin-top: 100px;
  max-width: 1280px;
  text-align: center;
}
img {
  margin-bottom: 1rem;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 90%;
}
li {
  margin: 0 0.5rem;
  padding: 0.25rem;
  font-size: 1.2rem;
}

nav {
  padding: 0 1rem;
}

a,
a:visited {
  text-decoration: none;
  color: inherit;
}

a:hover {
  color: #00c58e;
}
.wrapper{
    display:flex;
}
.wrapper > div {
    flex: 1;
}
.header {
  background-size: cover;
  min-height: 100vh;
}
.header .navbar {
  background-color: transparent !important;
}
.box {
  width: 180px;
  /* margin: 10%;
  padding: 10%; */
}
</style>
