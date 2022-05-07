<template>
  <div class="row">
      <div class="container">
      <h1>Log In</h1>
      <hr/>

      </div>

    <div v-if="errors" class="col s12 m7">
        <div class="card horizontal">
            <div class="card-stacked">
                <div class="card-content">
                <h4>Email / Password Invalidos</h4>
                </div>
            </div>
        </div>
    </div>


    <form @submit.prevent="validarUsuario" class="col s12">
      <div class="row">
                <div class="row">
                    <div class="input-field col s12">
                        <input v-model.trim="email" id="email" type="email" class="validate">
                        <label for="email">Email</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input v-model.trim="pass" id="password1" type="password" class="validate">
                        <label for="password">Password</label>
                    </div>
                </div>
                
            </div>
            <button type="submit" class="waves-effect waves-light btn">Log In</button>
        </form>
    </div>
</template>

<script>
import router from '../router/index'

export default {
    data(){
        return {
            email:"",
            pass:"",
            errors:false,
        }
    },
    methods:{
        async validarUsuario(){
            if(this.pass.length >= 6 && this.email != ""){

                const API_KEY = "AIzaSyAxuF_9CMPy-nyV2_6vGIZ4gJpY_P4TL6g";

                try{
                    const res = await fetch(`https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=${API_KEY}`, {
                        method: "POST",
                        body:JSON.stringify({
                            email: this.email,
                            password:this.pass,
                            returnSecureToken:true,
                        }),
                    });
                    const data = await res.json();

                    if(data.error){
                        this.errors = true;
                    }else{
                        this.errors = false;
                        localStorage.setItem("user",JSON.stringify(data));
                        router.push("/proyectos")
                    }
                    
                }catch(error){}
                
            }else{
                return;
            }
        }
    }
}
</script>

<style>

</style>