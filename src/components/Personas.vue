<script>
import axios from 'axios'

let API_URL = '/api/getPersonasUxd.php'

export default {

  data() {
    return {
      //variables de retorno  
      //para lista de personas
      personas: [],
      infoUno: [],


      //para ocultar y mostrar
      mostrarLista: false,
      mostrarBuscados: false,
      mostrarUno:false,
      nohay:false,

      //para el buscador
      buscar:"",
      buscados:[]
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
    //funcion para buscar personas por id
    buscador(buscar) { 

      //si esta vacio
      if(buscar==""){
        //muestra la lista
        this.mostrarLista= true
        //oculta la tarjeta de buscados
        this.mostrarBuscados = false
        //oculta mensaje no hay
        this.nohay=false
      }
      //sino
      else{
        //si se escribe algo entonces se oculta la lista
        this.mostrarLista= false
        
        //si es numerico
        if(!isNaN (buscar) === true) {
          //busca en el servidor por url
          API_URL='/api/getPersonasUxd.php?id='+ buscar

          //metodo get
          axios.get(API_URL) 
          //si hay error entonces
          .catch(error => {
            //oculta la card del buscado
            this.mostrarBuscados = false

            //muestra mensaje que no existe el id que busca
            this.nohay = true
          })
          //si no hay errores guarda todo lo que recibe 
          .then((response) => {
            //llamando a los datos del json extraido
            this.buscados = response.data.persona;
            //mostrando buscados en consola
            console.log(this.buscados)
            //mostramos cards buscados
            this.mostrarBuscados = true
            //deshabilitamos mensaje no existe
            this.nohay = false
            console.log(this.nohay)
          })         
        
          //cambiamos a verdadero que recibe por nombre 
          this.nohay=true           
        } 
           
      }
      
    },
    //informacion de una persona
    InfoPer(id) {  
      console.log("listaa", this.mostrarLista)   
      //url de consumo API
      API_URL='/api/getPersonasUxd.php?id='+id 
      console.log(API_URL)

      //lo obtiene
      axios.get(API_URL)

      //tomamos la respuesta
      .then((response) => {
        console.log(response) //regresa datos de una sola persona
        //contiene el array de cada persona con sus datos
        this.infoUno = response.data.persona;
        console.log(this.infoUno)
        this.mostrarLista = false 
        console.log(this.mostrarLista)
      })

      //el id incrementa
      this.id++
      //cambiamos el valor por verdadero para que lo muestre
      this.mostrarUno=true
      console.log(this.mostrarUno)

    },
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
      ENCONTRO VARIOS PERSONAS POR SU ID-->
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

  <!--si no existe el id buscado-->
  <div v-if="nohay" class="mx-auto">

    <!--Muestra mensaje de no existe-->
    <h1 class="text-center text-xl my-5">
      No existe el usuario que buscas :0
    </h1>

  </div>

  <!--TABLA-->
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
              <td class=" border-black border-2 mx-3  bg-white py-2 px-3"> <button @click="InfoPer(p.id)"> VER PERSONA </button> </td>
            </tr>
            
          </tbody>
        </table>

    </div>
        
  </div>

  <!--Informacion sólo Uno-->
  <div class="m-auto"  v-if="mostrarUno">
    
    <!--carta de personaje-->          
    <div class="w-3/4 mx-auto my-auto p-3 border-4 border-black bg-white rounded-sm">
      
      <h2> <b>Id: </b> {{ infoUno.id }}</h2>
      <h2> <b>Nombre:</b> {{ infoUno.nombre }}</h2>
      <h4> <b>Especie:</b> {{ infoUno.edad}}</h4>
      <h4> <b>Estado:</b> {{ infoUno.estadoCivil}}</h4>
      <h4> <b>Tipo:</b> {{ infoUno.trabajo }}</h4>
      <h4> <b>Locación:</b> {{ infoUno.residencia}}</h4>
    </div>
          
  </div>
</template>