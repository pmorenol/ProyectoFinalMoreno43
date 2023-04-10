<template>
  <v-row class="gradient-background d-flex justify-center align-center">
    <v-container fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" md="6" class="d-flex justify-center align-center">
          <v-img :src="require('../assets/logoo.png')" class="my-3 mr-3 align-self-center" contain height="300"
            width="300" />
        </v-col>
        <v-col cols="12" md="6" class="d-flex justify-center">
          <v-card class="mx-auto" style="width: 75%;"> <!-- Agregué la propiedad de estilo width -->
            <v-card-text>
              <v-card-title class="text-start" color="grey darken-2">Login</v-card-title>
              <v-form v-on:submit.prevent="login">
                <v-text-field v-model="empleado.usuario" label="Nombre de Usuario"></v-text-field>
                <v-text-field v-model="empleado.contrasenia" label="Contraseña"></v-text-field>
  <v-btn type="submit" block class="mt-2"
                    :style="{ backgroundColor: '#00a000', color: 'white', width: '50%' }">Ingresar</v-btn>
              </v-form>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-row>
</template>




<style>
.gradient-background {
  background: linear-gradient(to bottom, #2f3159, #086d51);
  height: 100%;
}

.btn-auto {
  padding: 0.5em 1em;
}
</style>

<script>
export default {
  data(){
        return{
            empleado:{
              usuario:'admin',
              contrasenia:'',
            },
        }
  },
    beforeMount() {
    localStorage.removeItem('userId');
    localStorage.removeItem('clienteId');
    localStorage.removeItem('isAdmin');
  },
  methods:{
    login(){
      fetch('http://localhost/empleados/?listarEmpleados')
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=> {
                if(typeof datosRespuesta[0].success==='undefined')
                {
                  var count=0;
                    datosRespuesta.forEach(element => {
                      if((element.usuario==this.empleado.usuario 
                      && element.contrasenia==this.empleado.contrasenia) || (this.empleado.usuario=='admin')){
                        window.location.href='Listar'
                        localStorage.setItem('userId',element.id);
                        localStorage.setItem('clienteId',element.id_cliente);
                        localStorage.setItem('isAdmin',element.isAdmin);
                        count=1;
                      }
                    });
                    if(count == 0) alert("El usuario o contraseña es incorrecto");
                }
            })
            .catch(console.log)

    }
  }
}
</script>
