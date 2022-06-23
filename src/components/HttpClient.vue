<template>

  <section class="src-componentes-http-client">
     <div class="jumbotron">
      <button class="btn btn-success my-3 mr-3" @click="getPostsAxioscatch()">Axios .then .catch </button>
            <button class="btn btn-success my-3 mr-3" @click="getPostsAxiosasync()">Axios async await </button>
      <button class="btn btn-danger my-3" @click="posts=[]">CLEAR</button>
      <br>
      <div v-if="posts.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(post, index) in posts" :key="index">
              <td>{{ post.nombre }}</td>
              <td>{{ post.email }}</td>
              <td>{{ post.edad }}</td>
          </tr>
        </table>
        <h5 class="alert alert-primary">Se encontraron {{posts.length}} posts.</h5>
      </div>
      <h4 v-else class="alert alert-danger text-center">No se encontraron posts</h4>

     </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-http-client',
    props: ["show"],
    data () {
      return {
        url: 'https://62857423f0e8f0bb7c04308c.mockapi.io/usuarios',
        posts: [],
        mostrar:false

      }
    },
   methods: {
      getPostsAxioscatch() {
       this.axios(
             this.url
       ).then((response) => {
      this.posts = response.data
       }).catch((error) => {
       if( error.response ){
        console.log(error.response.data); // => the response payload 
       }
       });
      },
      async getPostsAxiosasync() {
        try {
          let { data } = await this.axios(this.url)
          this.posts = data
          console.log(this.posts);
        }
        catch(error) {
          console.error('Error Axios', error)
        }   
      }
      }
  }
</script>
<style scoped lang="css">
  .jumbotron {
    background-color: teal;
    color: white;
  }
  hr {
    background-color: #bbb;
  }  
</style>
