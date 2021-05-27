<template>

  <section class="src-componentes-http">
    <div class="jumbotron">
      <h2>Usuarios Almacenados</h2>
      <hr>

      <button class="btn btn-danger my-3 mr-3" @click="getUsuariosCb()">Pedir XMLHttpRequest</button>    
      <button class="btn btn-warning my-3 mr-3" @click="getUsuariosFetch()">Pedir FETCH</button>    
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Pedir AXIOS</button>    

     

      <div v-if="usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Teléfono</th>
            <th>Email</th>
          </tr>
          <tr v-for="(usuario,index) in usuarios" :key="index">
            <td>{{usuario.nombre}}</td>
            <td>{{usuario.telefono}}</td>
            <td>{{usuario.email}}</td>
          </tr>

        </table>
        <h4 class="alert alert-primary">Se encontraron {{usuarios.length}} usuarios</h4>
      </div>
      <h4 v-else class="alert alert-danger">No se encontraron usuarios</h4>

    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-http',
    props: [],
    mounted () {

    },
    data () {
      return {
        //url : 'https://jsonplaceholder.typicode.com/usuarios',
        //url : 'https://jsonplaceholder.typicode.com/comments',
        url: 'https://60aeb65e5b8c300017deb20e.mockapi.io/usuarios',
        usuarios : []
        
      }
    },
    methods: {

      getUsuariosCb() {
        
        let xhr = new XMLHttpRequest
      
        xhr.open('get',this.url)
  
        xhr.addEventListener('load', () => {
          if(xhr.status == 200) {
            let respuesta = JSON.parse(xhr.response)
            console.log('XMLHttpRequest',respuesta)
            this.usuarios = respuesta
          }
          else {
            console.error(`Error en GET -> status: ${xhr.status}`)
          }
        })
        xhr.addEventListener('error', e => {
            console.error(`Error XMLHttpRequest ->`, e)
        })
      
        xhr.send()
      },

      getUsuariosFetch() {
          fetch(this.url)
          .then(datos => datos.json())
          .then(respuesta => {
            console.log('FETCH',respuesta)
            this.usuarios = respuesta
          })
          .catch(error => console.error(error))
      },

      getUsuariosAxios() {
          this.axios(this.url)
          .then( respuesta => {
            console.log('AXIOS', respuesta.data)
            this.usuarios = respuesta.data
          })
          .catch(error => console.error(error))
      }

    },
    computed: {
      getCols() {
        return Object.keys(this.usuarios[0])
      }
    }
}


</script>

<style scoped lang="css">
  .src-componentes-http {

  }

  .jumbotron {
    background: rgb(211,211,211); 
    color: white;
  }

  h2{
    color: black;
  }
     


  hr {
    background-color: #fff;
  }  
</style>