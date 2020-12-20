<template>

<v-app id="inspire">
    
 <v-app-bar app>
    <v-toolbar
    color="#1F618D "
    dark
  >
    <v-toolbar-title>MOMENTOS S.A</v-toolbar-title>

    <v-divider
      class="mx-4"
      vertical
    ></v-divider>

    

    <v-spacer></v-spacer>

    <v-toolbar-items class="hidden-sm-and-down">
       <v-btn text href="#elige">
        Elígenos
      </v-btn>
      <v-btn text href="#services">
        Nuestros servicios
      </v-btn>
      
      <v-btn text href="#testimonio">
        Testimonios
      </v-btn>


      <v-divider vertical></v-divider>

      <v-btn text href="/login" icon="mdi-login">
        Login
      </v-btn>

    </v-toolbar-items>

    
  </v-toolbar>
  </v-app-bar>

  
    <v-main>
      <v-container>
        <router-view />
         <v-carousel>
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
      reverse-transition="fade-transition"
      transition="fade-transition"
    ></v-carousel-item>
  </v-carousel>
     <h1 align="center">¿Por qué elegirnos?</h1>
    <v-row id='elige'>
     
       <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
    
    color="#FADBD8  "
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://i.pinimg.com/564x/0c/d8/51/0cd851ca388d28d4f538ce9324d46b39.jpg"
    ></v-img>


    <!-- Primera tarjeta -->
    <v-card-title>Pantallas LED de alta resolución</v-card-title>

    <v-card-text>
      

      <div class="my-4 subtitle-1">
        Llevamos a ti la mejor calidad
      </div>

      <div>Poseemos la más alta tecnología para la puesta en escena de conciertos, conferencias y eventos deportivos
        garantizando una excelente comunicación, además te brindamos asesoría para la transmisión de los eventos a nivel 
        nacional e internacional
      </div>
    </v-card-text> 

    
  </v-card>

   <!-- segunda tarjeta -->
    <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
    color="#FADBD8  "
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://i.pinimg.com/564x/f5/25/3a/f5253a99984fad727fdaf8e3a4c58c36.jpg"
    ></v-img>

    <v-card-title>Difusión en redes sociales</v-card-title>

    <v-card-text>
        <div class="my-4 subtitle-1">
        Los mejores profesionales
      </div>

      <div>Respondiendo a la importancia de las redes sociales, todo nuestro equipo está capacitado para difundir los distintos
        eventos atrayendo participantes y patrocinadores que harán brillar tu espectáculo
      </div>
    </v-card-text>

  </v-card>

  <!-- tercera tarjeta -->
   <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
    color="#FADBD8  "
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://i.pinimg.com/564x/50/35/5d/50355d4d8d59cc1477093a219d5252d5.jpg"
    ></v-img>

    <v-card-title>Cobertura a nivel nacional</v-card-title>

    <v-card-text>
        <div class="my-4 subtitle-1">
        Llegamos a todos los rincones del país
      </div>

      <div>Sabemos que muchos eventos necesitan logística de la más alta calidad, debido a esto brindamos 
        gestión e infraestructura de gran tecnología garantizando a todos nuestros clientes proyectos exitosos
      </div>
    </v-card-text>

    
  </v-card>
   
    </v-row>



    <h1 align="center">Nuestros servicios</h1>
    <div class="team">
      <v-container id='services' class="my-5" >
    <v-layout row wrap>
 
    <v-flex xs12 sm6 md4 lg3>
      <v-row>
        <v-col>
         <service-card
         v-for="(item,index) of services"
         :key="index"
         :service="item">
         </service-card>
         </v-col>
      </v-row> 
</v-flex>
  
  </v-layout></v-container>
    </div>

        </v-container>


  <h1 align="center">Testimonios</h1>
    <v-row id='testimonio'>
     
       <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
    
    color="#86EC9F  "
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://aguasmachala.gob.ec/wp-content/uploads/2018/08/Director-Financiero.jpg"
    ></v-img>


    <!-- Primera tarjeta -->
    <v-card-title>Banco BBVA</v-card-title>

    <v-card-text>
      

      <div class="my-4 subtitle-1">
        Gerente: Camilo Montenegro
      </div>

      <div>"El concierto para el aniversario de nuestro banco fue increíble, los músicos interpretaron piezas clásicas que fueron 
        conmovedoras para todos nuestros socios, además la atencipon brindada a los invitados fue de gran calidad"
      </div>
    </v-card-text> 

    
  </v-card>

   <!-- segunda tarjeta -->
    <v-card
    :loading="loading"
    class="mx-auto my-12"
    max-width="374"
    
    color="#86EC9F  "
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src="https://cdn.ticbeat.com/src/uploads/2019/09/GettyImages-1059661466-810x541.jpg"
    ></v-img>


    <!-- Primera tarjeta -->
    <v-card-title>Record sound</v-card-title>

    <v-card-text>
      

      <div class="my-4 subtitle-1">
        Gerente: Sofía Chávez
      </div>

      <div>"La conferencia de prensa de nuestra principal artista "JuliaX" fue muy satisfactoria, logramos mostrar su nuevo lanzamiento no solo a nivel nacional
        sino también a nivel mundial gracias al gran cubrimiento de telecomunicaciones que brindó Momentos S.A"
      </div>
    </v-card-text> 

    
  </v-card>

  </v-card>
   
    </v-row>

    </v-main>

  <v-footer
    dark
    height="auto"
  >
    <v-row>
      <v-col>
    <v-card
      class="flex"
      flat
      
    dark
      
    >
  

      <v-card-title class="teal">
        <strong class="subheading">Redes sociales: @momentos_s</strong>

        <v-spacer></v-spacer>

        <v-btn
          v-for="icon in icons"
          :key="icon"
          class="mx-3"
          dark
          icon
        >
          <v-icon size="24px">{{ icon }}</v-icon>
        </v-btn>
        <div>
          Visita nuestra sedes<br>
          Bogotá - Cr 56 #45-7A<br>
          Medellín - Cr 32 #21-12
          
          </div>
      </v-card-title>

      
    </v-card>
      </v-col>

      <v-col>
        <v-card
      class="flex"
      color="#26c6da"
   
     
    >
  

      <v-card-title class="teal" color="#26c6da">
        <strong class="heading">Contáctanos:</strong>

        <v-spacer></v-spacer>

       <div>
       
        Línea Nacional: 01 8000342981<br>
        Télefono: (+1) 3324567<br>
        E - mail: momentos_sa@enterprise.co<br>
        <br>
          </div>
          <v-icon size="24px">{{ icon }}</v-icon>
        </v-btn>
      </v-card-title>
    </v-card>
      </v-col>
    </v-row>
    <v-card
      class="flex"
      flat
      
    >
  
      <v-card-actions class="grey darken-3 justify-center">
        &copy;2020 — <strong>Momentos S.A</strong>
      </v-card-actions>
    </v-card>
  </v-footer>
  </v-app>
</template>

<script>
import ServiceCard from '../components/auth/ServiceCard.vue';
import Servicios from '../components/servicios.json';
  export default {
    name: 'HelloWorld',
    components:{
      ServiceCard,
    },

    data: () => ({
      
        services:Servicios,
      
     
    drawer: null,
    
      items: [
          {
            src: 'https://i0.wp.com/modoeficaz.com/wp-content/uploads/2018/10/Presentaciones-y-conferencias.jpg?fit=1800%2C1075&ssl=1',
          },
          {
            src: 'https://as01.epimg.net/colombia/imagenes/2019/09/10/tikitakas/1568074064_251138_1568074187_noticia_normal.jpg',
          },
          {
            src: 'https://www.elheraldo.co/sites/default/files/articulo/2016/07/14/peloton_ciclismo.jpg',
          },
          
        ],
        icons: [
        'mdi-facebook',
        'mdi-twitter',
        'mdi-linkedin',
        'mdi-instagram',
      ],
      
        
         
       
    
  }),
  }
</script>
