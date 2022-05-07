<template>
  <div class="container ">

      <div class="row m4">
          <router-link to="/proyectos" class="col s12 waves-effect waves-light w100 btn amber darken-3">
      <i class="material-icons">arrow_back</i>
                Regresar a lista de Proyecto
            </router-link>

        </div>

      <div class="row">
        <form @submit.prevent="updateProject" class="col s12">
            <div class="row">
                <div class="input-field col s12">
                    <input id="first_name" type="text" class="validate" placeholder="Nombre del Proyecto" v-model="project.title">
                    <label for="first_name"></label>
                </div>
                <div class="input-field col s12">
                    <input id="last_name" type="text" class="validate" placeholder="Description del Proyecto" v-model="project.description">
                    <label for="last_name"></label>
                </div>
                <p>
                    <label>
                        <input type="checkbox" checked="checked" v-model="project.langs" value="HTML"/>
                        <span >HTML</span>
                    </label>
                </p>
                
                <p>
                    <label>
                        <input type="checkbox" checked="checked" v-model="project.langs" value="CSS"/>
                        <span >CSS</span>
                    </label>
                </p>

                <p>
                    <label>
                        <input type="checkbox" checked="checked" v-model="project.langs" value="JavaScript"/>
                        <span >JavaScript</span>
                    </label>
                </p>

                <p>
                    <label>
                        <input type="checkbox" checked="checked" v-model="project.langs" value="Vue"/>
                        <span >Vue</span>
                    </label>
                </p>
                <button class="btn waves-effect waves-light col s12" 
                        type="submit" 
                        name="action">Submit
                        <i class="material-icons right">send</i>
                </button>
            </div>
        </form>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            project:{},
            id: this.$route.params.id
        };
    },
    mounted(){
        this.getProject();
    },
    methods:{
        async getProject(){
            const user = JSON.parse(localStorage.getItem("user"));
            const id = this.$route.params.id; 
            console.log(user)
    
            const res = await fetch(`https://crud-vue-eeddc-default-rtdb.firebaseio.com/projects/${user.localId}/${id}.json?auth=${user.idToken}`);
            const data = await res.json();
            this.project = data;
        },
        async updateProject(){
            const user = JSON.parse(localStorage.getItem("user"));
            const res = await fetch(`https://crud-vue-eeddc-default-rtdb.firebaseio.com/projects/${user.localId}/${this.id}.json?auth=${user.idToken}`,{
                method:"PATCH",
                body:JSON.stringify(this.project),
                
            });
            this.$router.push("/proyectos")
           // const data = await res.json();
        }
    }
}
</script>

<style>

</style>