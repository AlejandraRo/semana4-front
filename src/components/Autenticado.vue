<template>
<v-app id="inspire">
     <v-carousel>
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
      reverse-transition="fade-transition"
      transition="fade-transition"
    ></v-carousel-item>
  </v-carousel>
    <v-navigation-drawer
      v-model="drawer"
      app
    >
    <v-card
    class="mx-auto"
    max-width="300"
    tile
  >
    <v-list dense>
      <v-subheader>MOMENTOS S.A</v-subheader>
      <v-list-item-group
        v-model="selectedItem"
        color="primary"
      >
        <v-list-item
          v-for="(item, i) in lista"
          :key="i"
          :to="{name:item.ruta}"
          exact
        >
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title v-text="item.text"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-card>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer">

      </v-app-bar-nav-icon>

      <v-toolbar-title>Menú</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon
      class="mr-5"
      @click="salir()">
      <v-icon>mdi-logout</v-icon>
      <span>Salir</span>
      </v-btn>
      
    </v-app-bar>


  
    <v-main>
      <v-container>
        <router-view />
        </v-container>
    </v-main>
  </v-app>
</template>
<script>
  export default {
      name:'Autenticado',
      data: () => ({
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
       lista: [
        { text: 'Inicio', icon: 'mdi-home',ruta:'Home' },
        { text: 'Categorías', icon: 'mdi-alphabetical',ruta:'Categoria' },
        { text: 'Artículos', icon: 'mdi-animation',ruta:'Articulo' },
        { text: 'Usuarios', icon: 'mdi-account',ruta:'Usuario' },
      ],
    
  }),
  created(){
    this.$store.dispatch("autoLogin");
  },
  methods:{
    salir(){
      this.$store.dispatch("salir");
    }
  }

  }
</script>