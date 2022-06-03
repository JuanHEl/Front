<template>
  <div class="header">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <ul class="navbar-nav mr-auto my-2 my-lg-0">
        <div class="my-2">
          <h4 style="color:white" v-if="this.nombre">Bienvenido: {{nombre}}</h4>
        </div>
        <div class="wrapper my-2">
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/resumen">Resumen</NuxtLink>
                </li>
            </div>
            <div class="box">
                <li>
                    <NuxtLink style="color:white" to="/admins">Administradores</NuxtLink>
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
                    <NuxtLink style="color:white" to="/configuracion">Configuración Red</NuxtLink>
                </li>
            </div>
            <!-- <div class="box3">
                <li>
                    <NuxtLink style="color:white" to="/login">Login</NuxtLink>
                </li>
            </div> -->
        </div>
      </ul>
      <div class="form-group col-sm-2">
        <div class="dropdown">
          <b-button
          variant="primary"
          text="Info"
          class="m-md-2"
          ><b-icon icon="info-circle" style="color:white">
              </b-icon></b-button>
          <div class="dropdown-content">
            <b-button style="width:100%" variant="primary" class="btn btn-primary" v-on:click="setinfo" to="/login" v-b-tooltip.hover title="Cerrar Sesion">
              <b-icon icon="power" style="color:white">
              </b-icon>
            </b-button>
            <!-- <b-button type="button" class="btn btn-outline-primary my-2 my-sm-0">
              <b-icon icon="power" style="color:white">
              </b-icon>Perfil
            </b-button> -->
            <b-button style="width:100%" variant="primary" class="btn btn-primary" to="/perfil" v-b-tooltip.hover title="Editar">
              <b-icon icon="pencil" style="color:white">
              </b-icon>
            </b-button>
            <!-- <b-dropdown-item href="#">Perfil</b-dropdown-item>
            <b-dropdown-item href="#">Editar</b-dropdown-item> -->
          </div>
        </div>
      </div>
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
        return {
          nombre:"",
          mensaje:null
        };
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
          this.$cookies.remove('user');
        }
    },
    watch: {},
    mounted: function () {
      this.nombre=this.$cookies.get('user').Nombre_Usuario;
      let now = new Date();
      let options = {
          year: 'numeric',
          month: '2-digit',
          day: '2-digit',
          hour: '2-digit',
          minute: '2-digit',
          second: '2-digit'
      };
      let fecha= now.toLocaleString('sv-SE', options); 
      console.log(this.$cookies.get('user'));
      if (this.$cookies.get('user').Fecha_Ultimo_Cambio_Pass) {
        console.log('Usuario')
        console.log(this.$cookies.get('user').Fecha_Ultimo_Cambio_Pass)
        console.log('actual')
        console.log(fecha)
      }
      //   (makeToast,variant = null) =>{
      //     this.$bvToast.toast(this.mensaje, {
      //       title: "Mensaje",
      //       variant: variant,
      //       solid: true,
      //     })
      //   };
      }
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
  width: 195px;
  /* margin: 10%;
  padding: 10%; */
}
.dropdown {
  display: inline-block;
  position: relative;
}
.dropdown-content {
  display: none;
  position: absolute;
  width: 100%;
  box-shadow: 0px 10px 10px 0px rgba(0,0,0,0.4);
}
.dropdown:hover .dropdown-content {
  display: block;
}
.dropdown-content a {
  display: block;
  color: #000000;
  padding: 5px;
  background-color: primary;
  text-decoration: none;
}
.dropdown-content a:hover {
  color: #FFFFFF;
  background-color: primary;
}
</style>
