<template>
  <v-row class="gradients-background d-flex justify-center align-center">
<v-carousel>
  <v-carousel-item
    src="../assets/empresa.jpg"
    cover
  ></v-carousel-item>

  <v-carousel-item
      src="../assets/empresa01.jpg"
    cover
  ></v-carousel-item>

  <v-carousel-item
      src="../assets/empresa02.jpg"
    cover
  ></v-carousel-item>

</v-carousel>
<div>
<v-card
      class="center"
      width="1000"
      text="Tenemos más de 15 años en el mercado de tecnología, realizamos todo tipo de tareas desde hardware hasta software, no dude en contratar nuestros servicios"
></v-card>
<br>
<v-card
      class="center"
      width="1000"
      text="Brindamos asesoría y acompañamiento en manejo de finanzas y proyección escalable de proyectos productivos"
    ></v-card>
<br>

    <v-card
      class="center"
      width="1000"
      text="Ofrecemos servicios de calidad, los cuales se ajustan a la necesidad del cliente"
    ></v-card>
    <br>

              <router-link to="/Listar">
          <div class="pa-2">
            <v-btn block>
              Regresar
            </v-btn>
          </div>
          </router-link>
</div>
  </v-row>
</template>

<style>
.center {
  margin: auto;
  width: 60%;
  border: 3px solid #73AD21;
  padding: 10px;
}
.gradients-background {
  background: linear-gradient(to bottom, #404499, #d9ebe6);
  height: 100%;
}
</style>