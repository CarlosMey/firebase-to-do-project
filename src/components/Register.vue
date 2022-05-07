<template>
  <div class="row">
      <div class="container">
      <h1>Registrar</h1>
      <hr/>

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
                        <input v-model.trim="pass1" id="password1" type="password" class="validate">
                        <label for="password">Password</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input v-model.trim="pass2" id="password2" type="password" class="validate">
                        <label for="password">Confirm Password</label>
                    </div>
                </div>
            </div>
            <button type="submit" class="waves-effect waves-light btn">Register</button>
        </form>
    </div>
</template>

<script>
import router from '../router/index'
export default {
    data(){
        return {
            email:"",
            pass1:"",
            pass2:"",
        }
    },
    methods:{
        async validarUsuario(){
            if(this.pass1 === this.pass2 && this.pass1.length >= 6 && this.email != ""){

                const API_KEY = "AIzaSyAxuF_9CMPy-nyV2_6vGIZ4gJpY_P4TL6g"
                const res = await fetch(`https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=${API_KEY}`, {
                    method: "POST",
                    body:JSON.stringify({
                        email: this.email,
                        password:this.pass1,
                        returnSecureToken:true,
                    })
                });
                const data = await res.json();
                localStorage.setItem("user", JSON.stringify(data));
                router.push("/proyectos");
            }else{
                return;
            }
        }
    }
}
</script>

<style>

</style>