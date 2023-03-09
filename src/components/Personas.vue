<script>
import axios from 'axios'

let API_URL = '/api/getPersonasUxd.php'

export default {

  data() {
    return {
        //variables de retorno  
        //para lista de personas
        personas: [],
        mostrarLista: false,
        mostrarBuscados: false,
        nohay:false,
        buscar:"",
        buscados:[],
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
          this.mostrarLista= true
          this.mostrarBuscados = false
          
          
        }
        else{
          this.mostrarLista= false
          

          if(!isNaN (buscar) === true) {
          API_URL='/api/getPersonasUxd.php?id='+ buscar

          axios.get(API_URL) 
          .catch(error => {
             
             this.mostrarBuscados = false
             this.nohay = true
           })
          
          .then((response) => {
            
            this.buscados = response.data.persona;
            console.log(this.buscados)
            this.mostrarBuscados = true
            this.nohay = false
            
          })

          console.log(this.nohay)
          
          //cambiamos a verdadero que recibe por nombre 
          this.nohay=true           
          } 
               
        }
        
      }
    }
}
</script>

<template>

  <!--Buscador-->
  <div class="flex justify-center items-center space-x-4 text-base my-2">
    <input class="h-12 wl-5 px-7" type="text" v-model="buscar"  placeholder="Buscar por nombre o id" @input = "buscador(buscar)">

  </div>
    
  <!--Resultados Buscador-->


  <!--si no recibe true en la variable mostrarBuscados
      ENCONTRO VARIOS PERSONAJES POR SU NOMBRE-->
  <div v-if="mostrarBuscados">
   
    <!--Recorre la nueva lista y por cada personaje que encuentra-->    
    <div class=" my-5 mx-auto p-3 border-4 border-black bg-white rounded-sm text-black">
     
      <!--carta de personaje-->          
      <h2> <b>Id: </b> {{ buscados.id }}</h2>
      <h2> <b>Nombre:</b> {{ buscados.nombre }}</h2>
      <h4> <b>Edad:</b> {{ buscados.edad }}</h4>
      <h4> <b>Estado Civil:</b> {{ buscados.estadoCivil }}</h4>
     
    </div> 
    
  </div>

  <div v-if="nohay" class="mx-auto">

    <h1 class="text-center text-xl my-5">
      No existe el usuario que buscas :0
    </h1>

  </div>


  <!--Recorre la nueva lista y por cada personaje que encuentra-->    
  <div class="w-2/3 my-5 mx-auto p-3 border-4 rounded-lg bg-black mb-5 mt-6">

    <h1 class="text-center text-white text-4xl font-bold mt-4"> Lista de Personas</h1><br>
    
    <div class="text-2xl text-black mx-auto">
        
        <table class = "table border-black border-4 text-base mx-auto">
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
            <tr v-for="(p, index) in personas"  class=" border-black border-4">
              <td class=" border-black border-2 mx-3  bg-white py-2 px-3 ">  {{ index += 1 }} </td>
              <td class=" border-black border-2 mx-3  bg-white py-2 px-3">{{ p.nombre }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-2 px-3">{{ p.edad }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-2 px-3">{{ p.trabajo }}</td>
              <td class=" border-black border-2 mx-3  bg-white py-2 px-3">{{ p.residencia }}</td>
              
            </tr>
            
          </tbody>
        </table>

    </div>
        
  </div>
</template>