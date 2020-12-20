<template>

      <v-card
      id="services"
      :loading="loading"
      class="flexservice card"
      max-width="374"
      color="#86E7EC"
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
        :src="service.image"
      ></v-img>
  
      <v-card-title>{{service.nombre}}</v-card-title>
  
      <v-card-text>
        {{service.descripcion}}
       
 
      </v-card-text>
  
    </v-card>
  
  
 
</template>

<script>
export default {
    name: "ServiceCard",
    props: ['service']
};
</script>

<style scoped>
</style>