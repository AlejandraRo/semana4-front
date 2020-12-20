<template>

<v-data-table
    :headers="headers"
    :items="usuarios"
    sort-by="id"
    class="elevation-1"
    :loading="cargando"
    loading-text="Cargando...por favor espere"
    color="#B3CEF2"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Usuarios</v-toolbar-title>
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
              Agregar Usuario
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
                      v-model="editedItem.name"
                      label="Nombre"
                    ></v-text-field>
                  </v-col>
                  
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.email"
                      label="email"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.estado"
                      label="estado"
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
     name:'DataUser',
    data: () => ({
      dialog: false,
      dialogDelete: false,
      cargando:true,
      headers: [
        { text: 'ID', value: 'id' },
        {
          text: 'Nombre',
          align: 'start',
          sortable: true,
          value: 'name',
        },
        { text: 'Correo', value: 'email' },
        { text: 'Estado', value: 'estado' },
        
        { text: 'Actions', value: 'actions', sortable: false },
      ],
   
      usuarios:[],
      editedIndex: -1,
      editedItem: {
        id:0,
        name: '',
        email: '',
        estado:'',
        
      },
      defaultItem: {
         id:0,
        name: '',
        email: '',
        estado:'',
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Nueva categoría' : 'Editar Categoría'
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
      this.initialize();
      this.list();
    },

    methods: {
      initialize () {
        this.desserts = [
          {
            nombre: 'Frozen Yogurt',
            descripcion: 159,
            estado: 6.0
          },
        ]
      },
      list()
      {
            axios.get('http://localhost:3000/api/usuario/list',{
              headers:{
                token:this.$store.state.token
              }
            })
            .then(response=>{
                this.usuarios=response.data;
                
                this.cargando=false;
            })
            .catch(error=>{
                console.log(error);
                return errror;
            })
      },

      editItem (item) {
        this.editedIndex = item.id
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
          axios.put("http://localhost:3000/api/categoria/deactivate",{"id":this.editedItem.id,})
          .then(response => {
            this.list();
          })
          .catch(error => {
            return error;
            console.log(error);
          })

        } else {
          axios.put("http://localhost:3000/api/categoria/activate",{"id":this.editedItem.id,})
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
          this.editedItem = Object.assign({}, this.defaultItem)
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
          axios.put("http://localhost:3000/api/categoria/update",{"id":this.editedItem.id,
          "nombre":this.editedItem.name,"descripcion":this.editedItem.descripcion})
          .then(response => {
            this.list();
          })
          .catch(error => {
            return error;
            console.log(error);
          })

        } else {
          axios.post("http://localhost:3000/api/categoria/add",{
          "nombre":this.editedItem.name,"descripcion":this.editedItem.descripcion,
          "estado":1})
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