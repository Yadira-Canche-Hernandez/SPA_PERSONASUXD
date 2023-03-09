<script>
import axios from 'axios'

let API_URL = '/api/getPersonasUxd.php'

export default {

  data() {
    return {
        //variables de retorno  
        //para lista de personas
        personas: [],
      }
    },
    mounted() {
      axios
        .get(API_URL)
          .then((response) => {
          
          //lista
          this.personas = response.data.personas
          console.log (this.personas)
      })
  },
}
</script>

<template>
<!--Recorre la nueva lista y por cada personaje que encuentra-->    
<div class=" my-5 mx-auto p-3 border-4 border-black bg-white rounded-sm">
      
    <div class="text-2xl my-10 text-black mx-5 sm:py-2" >
        <h1 > Lista de Personas</h1><br>
        <ul class="text-lg">
          <li v-for="p in personas">
            <!--Llamando función obtener info personal por personaje-->
            <button @click=""> {{ p.id }}. {{ p.nombre }} </button> 
          </li>
        </ul>
      </div>
      
    </div>
</template>