<template>
  
    <div>

        
  <nav>
    <div class="nav-wrapper light-blue">
      <router-link class="brand-logo" to="/">Gestor de Proyectos</router-link>
      
      <a href="#" data-target="mobile-demo" class="sidenav-trigger">
          <i class="material-icons">menu</i></a>
      <ul class="right hide-on-med-and-down">
        <li>
          <router-link v-if="!sesion" to="/">Registrar</router-link>
        </li>

        <li>
          <router-link v-if="!sesion" to="/login">Log In</router-link>
        </li>
        
        <li>
          <router-link v-if="sesion" to="/proyectos" class="waves-effect waves-light btn red lighten">
            Proyectos
          </router-link>
        </li>

        <li>
          <router-link v-if="sesion" to="/" @click="cerrarSesion" class="waves-effect waves-light btn red lighten">
            Cerrar sesion
          </router-link>
        </li>
      </ul>
    </div>
  </nav>

  <ul class="sidenav" id="mobile-demo">
    <li>
          <router-link v-if="!sesion" to="/">Registrar</router-link>
        </li>

        <li>
          <router-link v-if="!sesion" to="/login">Log In</router-link>
        </li>

        <li>
          <router-link v-if="sesion" to="/proyectos" class="waves-effect waves-light btn">
            Proyectos
          </router-link>
        </li>

        <li>
          <router-link v-if="sesion" to="/" @click="cerrarSesion" class="waves-effect waves-light btn red lighten">
            Cerrar sesion
          </router-link>
        </li>
        
  </ul>
    </div>
</template>

<script>
export default {
    name:"navbarComponents",
    data:()=>({
      user:false,

    }),

    mounted(){
      M.AutoInit();
    },
    methods:{
      cerrarSesion(){
        localStorage.removeItem("user");
      }
    },

    computed:{
      sesion(){
        const user = localStorage.getItem("user")
        if(user){
          return true
        }else{
          return false
        }
      }
    }
}
</script>

<style>

</style>