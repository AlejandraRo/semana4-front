<template>

<v-data-table
    :headers="headers"
    :items="articulos"
    sort-by="id"
    class="elevation-1"
    :loading="cargando"
    loading-text="Cargando...por favor espere"
    color="#F9DF94"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Artículos</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="500px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              Agregar Articulo
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.id"
                      label="ID"
                    ></v-text-field>
                  </v-col>

                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.nombre"
                      label="Nombre articulo"
                    ></v-text-field>
                  </v-col>

                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-select
                      v-model="categoria"
                      label="Categoria"
                      :items="categorias"
                      item-text="nombre"
                      item-value="id"
                      return-object
                    ></v-select>
                  </v-col>


                  <v-col
                    cols="12"
                    sm="12"
                    md="12"
                  >
                    <v-textarea
                      v-model="editedItem.descripcion"
                      label="Descripción"
                      counter="254"
                      no-resize
                    ></v-textarea>
                  </v-col>

                  <v-col
                    cols="12"
                    sm="12"
                    md="12"
                  >
                    <v-text-field
                      v-model="editedItem.codigo"
                      label="Codigo"
                      
                    ></v-text-field>
                  </v-col>

                  <v-col
                    cols="12"
                    sm="12"
                    md="12"
                  >
                    <v-text-field
                      v-model="editedItem.estado"
                      label="Estado"
                      
                    ></v-text-field>
                  </v-col>
                  
                  
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancelar
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Guardar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline">Está seguro que desea cambiar el estado?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
      <template v-if="item.estado">
          mdi-toggle-switch
      </template>

      <template v-else>
         mdi-toggle-switch-off-outline
      </template>
      
        
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<script>
import axios from 'axios';
  export default {
    name:'DataArticulo',
    data: () => ({
      dialog: false,
      dialogDelete: false,
      cargando:true,
      headers: [
        { text: 'ID', value: 'id' },
        {
          text: 'Articulo',
          align: 'start',
          sortable: true,
          value: 'nombre',
        },
        { text: 'Categoria', value: 'categoria.nombre' },
        { text: 'Descripcion', value: 'descripcion' },
        { text: 'Codigo', value: 'codigo' },
        
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      
      articulos:[],
      categoria:'',
      categorias:[],
      editedIndex: -1,
      editedItem: {
        id:0,
        nombre: '',
        descripcion: '',
        codigo:'',
        categoria:{
          id:0,
          nombre:'',
        },
        estado:0,
        
      },
      defaultItem: {
        id:0,
        nombre: '',
        descripcion: '',
        codigo:'',
        categoria:null,
        estado:0,
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Nuevo artículo' : 'Editar Artículo'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      
      this.list();
      this.listCategorias();
    },

    methods: {
     
      list()
      {
            axios.get('http://localhost:3000/api/articulo/list')
            .then(response=>{
                this.articulos=response.data;
                
                this.cargando=false;
            })
            .catch(error=>{
                console.log(error);
                return errror;
            })
      },
      listCategorias()
      {
            axios.get('http://localhost:3000/api/categoria/list',{
              headers:{
                token:this.$store.state.token
              }
            })
            .then(response=>{
                this.categorias=response.data;
                
            })
            .catch(error=>{
                console.log(error);
                return errror;
            })
      },

      editItem (item) {
        this.editedIndex = item.id
        this.categoria=item? item.categoria:''
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = item.id
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
       if (this.editedItem.estado===1) {
          axios.put("http://localhost:3000/api/articulo/deactivate",{"id":this.editedItem.id,},{
              headers:{
                token:this.$store.state.token
              }
            })
          .then(response => {
            this.list();
          })
          .catch(error => {
            return error;
            console.log(error);
          })

        } else {
          axios.put("http://localhost:3000/api/articulo/activate",{"id":this.editedItem.id,},{
              headers:{
                token:this.$store.state.token
              }
            })
          .then(response => {
            this.list();
          })
          .catch(error => {
            return error;
            console.log(error);
          })
          
        }
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem);
          this.categoria='';
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          axios.put("http://localhost:3000/api/articulo/update",
          {"id":this.editedItem.id,
          "nombre":this.editedItem.nombre,
          "descripcion":this.editedItem.descripcion,
          "codigo":this.editedItem.codigo,
          "categoriaId":this.categoria.id,},{
              headers:{
                token:this.$store.state.token
              }
            })
          .then(response => {
            this.list();
          })
          .catch(error => {
            return error;
            console.log(error);
          })

        } else {
          axios.post("http://localhost:3000/api/articulo/add",{
          "nombre":this.editedItem.nombre,
          "descripcion":this.editedItem.descripcion,
          "codigo":this.editedItem.codigo,
          "categoriaId":this.categoria.id,
          "estado":1},{
              headers:{
                token:this.$store.state.token
              }
            })
          .then(response => {
            this.list();
          })
          .catch(error => {
            return error;
            console.log(error);
          })
          
        }
        this.close()
      },
    },
  }
</script>