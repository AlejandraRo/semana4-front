<template>
    <v-container >
        <v-layout >
        <v-flex>
            <v-row
            align="center"
            align-content="center"
            style="height:70vh"
            class="mx-auto"
            
            >
                <v-col>
                    <v-card class="pa-10" color="#869CEC">
                        <v-card-title><br>Ingreso</br></v-card-title>
                        <v-form
                            ref="form"
                            
                            lazy-validation
                        >
                            
                            <v-text-field
                            v-model="login.email"
                            
                            label="E-mail"
                            required
                            ></v-text-field>
                            <v-text-field
                            v-model="login.password"
                            label="Contraseña"
                            type="password"
                            required
                            ></v-text-field>

                            
                            <v-btn
                            :disabled="!(this.login.email && this.login.password)"
                            color="success"
                            class="mr-4"
                            block
                            @click="loginUser"
                            >
                            Login
                            </v-btn>

                            
                        </v-form>
                    </v-card>
                </v-col>
            </v-row>
        </v-flex>
    </v-layout>
    </v-container>
</template>
<script>
import swal from "sweetalert";
import axios from 'axios';
export default {
     name:'login',
 data() {
 return {
 login: {
     user:"",
 email: "",
 password: ""
 }
 };
 },
  beforeCreate(){
    this.$store.dispatch("autoLogin");
  },
 methods: {
  loginUser() {

     axios.post("http://localhost:3000/api/usuario/login",this.login, {
         headers: {

         }
     })
     .then(response=>{
         return response.data;
     })
     .then(data => {
         this.$store.dispatch("guardarToken",data.tokenReturn);
         this.$router.push({name: 'Autenticacion'})
         console.log(data);
         swal("Exitoso", "El acceso fue exitoso", "success");
     })
     .catch(error => {
         swal("Error", "Datos inválidos", "error");
         console.log(error);
         return error;
     })
 }
 }
};
</script>