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
          
          //lista como en el json
          this.personas = response.data.personas
          console.log (this.personas)
      })
    },
    methods: {
      //funcion para buscar personajes
      buscador(buscar)  { 
        if(buscar==""){
          this.mostrarListas= true
          this.mostrarBuscados = false
          this.mostrarBuscadoID = false
        }
        else{
          this.mostrarListas= false
          console.log(!isNaN (buscar)) //comprobando que funcione con la funcion isNan
          //si lo que recibe del input es un numero
          if(!isNaN (buscar) === true) {
            //busca al personaje por su id
            API_URL='https://rickandmortyapi.com/api/character/'+buscar
            axios.get(API_URL) //usando axios
            .then((response) => {
              //toma todos los personajes que encuentra en resultados y lo almacena en la variable buscados
              console.log(response.data)
              this.buscado = response.data;
              console.log(this.buscado)
            })
            //si es por ir para que muestre
            this.mostrarBuscadoID = true
            //mantenemos en falso para que no muestre datos de la tarjeta de todos los personajes
            this.mostrarBuscados = false
          }
          
          //si no es numerico
          else{
            
            //lo busca por nombre                
            API_URL='https://rickandmortyapi.com/api/character/?name='+buscar
            axios.get(API_URL) //usando axios
            .then((response) => {
              //toma todos los personajes que encuentra en resultados y lo almacena en la variable buscados
              this.buscados = response.data.results;
              console.log(this.buscados)
              
            })
            //devolvemos falso por id
            this.mostrarBuscadoID = false
            //cambiamos a verdadero que recibe por nombre 
            this.mostrarBuscados = true
            
            }
              console.log(API_URL) //comprobando API_URL en consola
          }
      },
    }
}
</script>

<template>
<!--Recorre la nueva lista y por cada personaje que encuentra-->    
<div class="w-2/3 my-5 mx-auto p-3 border-4 rounded-lg bg-black mb-5">
    <h1 class="text-center text-white text-4xl font-bold mt-4 "> Lista de Personas</h1><br>
    
    <div class="text-2xl my-5 text-black mx-auto" >
        
        
        <table class = "table stripped bordered border-black border-4 text-base mx-auto">
          <thead >
            <tr class="border-black border-4 bg-emerald-500">
              <th class="border-black border-4">Id</th>
              <th class="border-black border-4">Nombre</th>
              <th class="border-black border-4">Edad</th>
              <th class="border-black border-4">Trabajo</th>
              <th class="border-black border-4">Residencia</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="p in personas" class=" border-black border-4">
              <td class=" border-black border-2 mx-3  bg-white py-3 px-3 ">{{ p.id }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-3 px-3">{{ p.nombre }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-3 px-3">{{ p.edad }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-3 px-3">{{ p.trabajo }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-3 px-3">{{ p.residencia }}</td>
            </tr>
          </tbody>
        </table>

      </div>
      
    </div>
</template>