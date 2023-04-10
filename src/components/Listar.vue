<template>
  <v-app-bar app :style="{ background: 'linear-gradient(to right, #05110F, #062722, #093524)' }">
    <v-app-bar-nav-icon color="white" @click="drawer = !drawer"></v-app-bar-nav-icon>
    <v-toolbar-title style="color: white;">Proyecto</v-toolbar-title>
  </v-app-bar>

  <v-navigation-drawer
    v-model="drawer"
    class="teal-lighten-4"
    theme="dark"
    hide-overlay
    width="300"
    app
  >

  <v-list color="transparent">
    <router-link to="/entidad">
      <v-list-item prepend-icon="mdi-view-dashboard" title="Quienes somos"></v-list-item>
    </router-link>
    <router-link to="/servicios">
      <v-list-item prepend-icon="mdi-account-box" title="Servicios"></v-list-item>
    </router-link>
  </v-list>
</v-navigation-drawer>
<div>


<v-sheet class="gradient-background">
  
  <v-container class="bg-gradient" style="min-height: 100vh">
  <v-container style="height: 100%">
  
  <v-container class="d-flex justify-center align-center">
    <v-container class="bg-surface-variant" align-content="center">
        <v-container class="bg-surface-variant mt-10">
      <v-container>
        <v-card class="mx-auto red-gradient-background"></v-card>
        <v-container class="bg-red-gradient">
  <v-container>
    <v-container class="bg-surface-variant text-center">
            <div v-if="isAdmin == 1">
      <router-link to="/crear">
        <v-container class="bg-gradient"></v-container>
        <v-btn color="success" class="me-4" to="/crear">
          Agregar nuevo empleados
        </v-btn>
      </router-link>
            </div>
      <br /><br />
      <v-card class="mx-auto">
        <v-card-title>Lista de empleados</v-card-title>
        <v-table dense>
          <thead>
            <tr>
              <th class="text-left">Nombre</th>
              <th class="text-left">Correo</th>
              <th class="text-left">Celular</th>
              <th class="text-left">Cargo</th>
              <th class="text-left">Usuario</th>
              <th class="text-left">Nombre del cliente</th>
              <th class="text-left">Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="empleado in empleados" :key="empleado.id">
              <td class="text-left">{{empleado.nombre}}</td>
              <td class="text-left">{{empleado.correo}}</td>
              <td class="text-left">{{empleado.celular}}</td>
              <td class="text-left">{{empleado.cargo}}</td>
              <td class="text-left">{{empleado.usuario}}</td>
              <td class="text-left">{{empleado.nombreCliente}}</td>
              <td>
                <router-link :to="{name:'Editar',params:{id:empleado.id}}">
                  <v-btn color="info" class="me-4" :to="{name:'Editar',params:{id:empleado.id}}">
                    Editar
                  </v-btn>
                </router-link>
                <v-btn
                  v-on:click="borrarEmpleado(empleado.id)"
                  class="me-4"
                  color="danger"
                  type="button"
                >
                  Borrar
                </v-btn>
              </td>
            </tr>
          </tbody>
        </v-table>
      </v-card>
      <br /><br />
      <v-card class="mx-auto">
        <router-link to="/crearCliente">
          <v-btn color="success" class="me-4" to="/crearCliente">
            Agregar nuevo cliente
          </v-btn>
        </router-link>
        <br /><br />
      <v-card-title>Lista de clientes</v-card-title>
        <v-table dense>
          <thead>
            <tr>
              <th class="text-left">Nombre</th>
              <th class="text-left">Nit</th>
              <th class="text-left">celular</th>
              <th class="text-left">Dirección</th>
              <th class="text-left">Tipo</th>
              <th class="text-left">Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="cliente in clientes" :key="cliente.id">
              <td class="text-left">{{cliente.nombre}}</td>
              <td class="text-left">{{cliente.nit}}</td>
              <td class="text-left">{{cliente.celular}}</td>
               <td class="text-left">{{cliente.direccion}}</td>
              <td class="text-left">{{cliente.tipoEmpresa}}</td>
              <td>
              <router-link :to="{name:'EditarCliente',params:{id:cliente.id}}">
              <v-btn color="info" class="me-4" :to="{name:'EditarCliente',params:{id:cliente.id}}">
              Editar
              </v-btn>
              </router-link>
              <v-btn
              v-on:click="borrarCliente(cliente.id)"
              class="me-4"
              color="danger"
              type="button"
              >
              Borrar
              </v-btn> 
              </td>
            </tr>
         </tbody>
        </v-table>    
      </v-card>
    </v-container>
</v-container>
  </v-container>
    </v-container>            
</v-container>

</v-container>
</v-container>

</v-container>


</v-container>

</v-sheet>  
</div>
</template>

<style>


.bg-surface-variant {
    background: linear-gradient(to bottom right, #160214, #052213);
}

 .gradient-background {
  background: linear-gradient(to bottom right, #091411, #0e1f1a, #072218, #052521, #1d1d1d);
  height: 100vh;
}

.header {
  width: 100%;
  background: linear-gradient(to right,#070f0d, #0a1a14, #070f0d);
}

.mx-auto {
  background: linear-gradient(to bottom, #b4dbbd, #ffffff);
}

.red-gradient-background {
  background: linear-gradient(to right, #ff5252, #d13239);
}

</style>


<script>


export default {
    data(){
        return{
          drawer: false,
            empleados:[],
            clientes:[],
            userId:null,
            isAdmin:null,
            clienteId:null,
        }

    },
     created:function(){
        this.clienteId=localStorage.getItem('clienteId'),
        this.userId=localStorage.getItem('userId'),
        this.isAdmin=localStorage.getItem('isAdmin'),
        this.consultarEmpleado();
        this.consultarClientes();
    },
    methods:{
        consultarEmpleado(){
            fetch('http://localhost/empleados/?consultarClientePorUsuario')
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=> {
                if(typeof datosRespuesta[0].success==='undefined')
                {
                    if(this.isAdmin==0){
                    datosRespuesta.forEach(element => {
                        if(element.id==this.userId){
                           this.empleados.push(
                            {
                            id:element.id,    
                            nombre:element.nombre,correo:element.correo,
                            celular:element.celular,cargo:element.cargo,
                            usuario:element.usuario,nombreCliente:element.nombreCliente,
                            });
                        }
                    });
                    }else{
                    this.empleados=datosRespuesta;
                    }
                   
                }
            })
            .catch(console.log)
        },
        borrarEmpleado(id){
            console.log(id);
            fetch('http://localhost/empleados/?borrar='+id)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=> {
                console.log(datosRespuesta)
                window.location.href='Listar'
            })
            .catch(console.log)
        },
        consultarClientes(){
            fetch('http://localhost/empleados/?listarClientes')
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=> {
                this.clientes=[]
                if(typeof datosRespuesta[0].success==='undefined')
                {
                    if(this.isAdmin==0){
                    datosRespuesta.forEach(element => {
                         if(element.id==this.clienteId){
                            this.clientes.push({
                                id:element.id,nombre:element.nombre,
                                nit:element.nit,direccion:element.direccion,
                                celular:element.celular,tipoEmpresa:element.tipoEmpresa,
                            })
                         }
                    });
                    }else{
                     this.clientes=datosRespuesta;
                    }
                 
                }
            })
            .catch(console.log)
        },
        borrarCliente(id){
            console.log(id);
            fetch('http://localhost/empleados/?borrarCliente='+id)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=> {
                console.log(datosRespuesta)
                window.location.href='Listar'
            })
            .catch(console.log)
        },
    }
}
</script>