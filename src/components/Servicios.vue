<template>
  <v-row class="gradient-background d-flex justify-center align-center">
  <v-card max-width="448" class="mx-auto">
    <v-layout>
      <v-main>
        <v-container fluid>
          <v-card
            border
            class="mb-2"
            density="compact"
            subtitle="Preventivo, Operativo"
            title="Mantenimiento de computadores"
            variant="text"
          >
            <v-img src="../assets/mantenimiento.png" height="128" cover></v-img>

            <v-card-text>
              Mantenimiento oportuno de computadores de mesa y portatiles, se utiliza el windows 10/11 con licencia para programas office, el servicio cuenta con garantia.
            </v-card-text>
          </v-card>

          <v-card
            border
            density="comfortable"
            subtitle="Mantenimiento,Redes,Seguridad"
            title="Servidores"
            variant="text"
          >
            <v-img src="../assets/servidor.jpg" height="128" cover></v-img>

            <v-card-text>
              Se brinda seguridad a tráves de back-up que permitan resguardar la información importante, también se ofrece soporte para alojamiento de proyectos digitales, y se realiza mantenimiento a servidores del cliente.
            </v-card-text>
          </v-card>

         <v-card
            border
            density="comfortable"
            subtitle="Base de datos,Proyectos digitales, Soporte y Versionamiento"
            title="Software"
            variant="text"
          >
            <v-img src="../assets/software.jpg" height="128" cover></v-img>

            <v-card-text>
              Según la necesidad del cliente se llevan a cabo desarrollos digitales, con tecnología moderna que permita estar al frente del mercado.
            </v-card-text>
          </v-card>



        </v-container>
      </v-main>
    </v-layout>
                <router-link to="/Listar">
          <div class="pa-2">
            <v-btn block>
              Regresar
            </v-btn>
          </div>
          </router-link>
  </v-card>

  </v-row>
</template>

<style>
.gradient-background {
  background: linear-gradient(to bottom, #2f3159, #086d51);
  height: 100%;
}
</style>
