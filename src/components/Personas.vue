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
      mostrarLista: true,
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
        if (this.infoUno.estadoCivil== 1){
          this.infoUno.estadoCivil= "Soltero"
        }
        if (this.infoUno.estadoCivil== 2){
          this.infoUno.estadoCivil= "Casado"
        }
        if (this.infoUno.estadoCivil== 3){
          this.infoUno.estadoCivil= "Divorciado"
        }
        if (this.infoUno.estadoCivil== 4){
          this.infoUno.estadoCivil= "Separado"
        }
        if (this.infoUno.estadoCivil== 5){
          this.infoUno.estadoCivil= "Unión libre"
        }
        if (this.infoUno.estadoCivil== 6){
          this.infoUno.estadoCivil= "Viudo"
        }
        console.log(this.infoUno)
         
      })

      //el id incrementa
      this.id++
      //cambiamos el valor por verdadero para que lo muestre
      this.mostrarUno=true
      //console.log(this.mostrarUno)
       
    },
  }

}
</script>

<template>

  <!--Buscador-->
  <div class="flex justify-center items-center space-x-4 text-base my-2 mx-auto">
    <label for="">Buscar</label>
    <input class="h-12 wl-5 px-7" type="text" v-model="buscar"  placeholder="Buscar por nombre o id" @input = "buscador(buscar)">

  </div>
    
  <!--Resultados Buscador-->

  <!--si no recibe true en la variable mostrarBuscados
      ENCONTRO VARIOS PERSONAS POR SU ID-->
  <div v-if="mostrarBuscados" class="m-auto w-3/4 mb-5">
   
    <!--Recorre la nueva lista y por cada personaje que encuentra-->    
    <!--carta de personaje-->          
    <div class="w-3/4  p-3 border-4 border-black bg-white rounded-sm">

      <!-- Información personal -->
      <div class="w-full mt-4 bg-lime-100  rounded-md ">
        <h1 class="text-2xl  text-center font-bold  text-black">Información personal</h1>

        <h2 class="mb-1 px-3"> <b>Id: </b> {{ buscados.id }}</h2>
        <h2 class="mb-1 px-3"> <b>Nombre:</b> {{ buscados.nombre }}</h2>
        <h4 class="mb-1 px-3"> <b>Especie:</b> {{ buscados.edad}}</h4>
        <h4 class="mb-1 px-3"> <b>Estado Civil:</b> {{ buscados.estadoCivil}}</h4>
        <h4 class="mb-1 px-3"> <b>Tipo:</b> {{ buscados.trabajo }}</h4>
        <h4 class="mb-1 px-3"> <b>Locación:</b> {{ buscados.residencia}}</h4>
      </div>

      <!-- Cita -->
      <div class="w-full mt-4 bg-orange-100 rounded-md">
        <h1 class="text-2xl  text-center font-bold  text-black">Frase</h1>
        <h4 class="mb-1 px-3"> <b>Cita:</b> <br> {{ buscados.cita}}</h4>
        <h4 class="mb-1 px-3"> <b>Autor:</b> {{ buscados.citaAutor}}</h4>
        
      </div>


      <!-- Personal -->
      <div class="w-full mt-4  bg-indigo-100 rounded-md">
        
        <h1 class="text-2xl  text-center font-bold  text-black">Biografía</h1>
          
        <h4 class="mb-1 px-3"> <b>Yo:</b> <br>{{ buscados.bio}}</h4>
      </div>

      <!-- Personalidades-->
      <div class="w-full mt-4 bg-fuchsia-200 rounded-md ">
        <h1 class="text-2xl  text-center font-bold  text-black">Personalidades</h1>

        <div class="w-full mt-4 mx-auto px-3 ">
          <label class=" text-black font-bold md:text-left my-2 md:mb-0">
              "Mente"  
              <br>
          </label>

          <div class="flex  justify-between px-4">
            <label class="text-black  text-left md:text-left my-2 md:mb-0">
              Extrovertido: <br>  {{buscados.personalidad01 }}%
            </label>
            
            <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
              Introvertido: <br> {{ 100 - buscados.personalidad01}}%
            </label>
          </div>

          <div class=" px-4">
          <input type="range" v-model="buscados.personalidad01" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
          </div>

        </div>

        <div class="w-full mt-4 mx-auto px-3">
            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                "Energia"  
                <br>
            </label>

            <div class="flex  justify-between px-4">
              <label class="text-black  text-left md:text-left my-2 md:mb-0">
                Intuitivo: <br>  {{buscados.personalidad02 }}%
              </label>
              
              <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
                Observador: <br> {{ 100 - buscados.personalidad02}}%
              </label>
            </div>
            <div class=" px-4">
            <input type="range" v-model="buscados.personalidad02" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
            </div>

        </div>

        <div class="w-full mt-4 mx-auto px-3">
          <label class=" text-black font-bold md:text-left my-2 md:mb-0">
              "Naturaleza"  
              <br>
          </label>

          <div class="flex  justify-between px-4">
            <label class="text-black  text-left md:text-left my-2 md:mb-0">
              Pensamiento: <br>  {{buscados.personalidad03 }}%
            </label>
            
            <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
              Emocional: <br> {{ 100 - buscados.personalidad03}}%
            </label>
          </div>
          <div class=" px-3">
          <input type="range" v-model="buscados.personalidad03" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
          </div>

        </div>

        <div class="w-full mt-4 mx-auto px-3">
          <label class=" text-black font-bold md:text-left my-2 md:mb-0">
              "Identidad"  
              <br>
          </label>

          <div class="flex  justify-between px-3">
            <label class="text-black  text-left md:text-left my-2 md:mb-0">
              Asertivo: <br>  {{buscados.personalidad04 }}%
            </label>
            
            <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
              Cauteloso: <br> {{ 100 - buscados.personalidad04}}%
            </label>
          </div>
          <div class=" px-3">
          <input type="range" v-model="buscados.personalidad04" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
          </div>

        </div>
      </div>

      <!-- Objetivos -->
      <div class="w-full mt-4  bg-yellow-100 rounded-md">
        
        <h1 class="text-2xl  text-center font-bold  text-black">Objetivos</h1>
        
        <!-- recorro array de objetivos y llamo a index -->
        <div class="w-full mt-4 mx-auto px-3" v-for="o,index in buscados.objetivos">

          <label class=" text-black font-bold md:text-left my-2 md:mb-0">
              Objetivo {{ index +1 }}:
              <br>
          </label>

          <h4 class="mb-1 px-3">{{ o.objetivo }}</h4>

        </div>

      </div>

      <!-- Frustraciones -->
      <div class="w-full mt-4  bg-red-100 rounded-md">
        
        <h1 class="text-2xl  text-center font-bold  text-black">Frustracionees</h1>
        
        <!-- recorro array de frustraciones y llamo a index -->
        <div class="w-full mt-4 mx-auto px-3" v-for="f,index in buscados.frustraciones">

          <label class=" text-black font-bold md:text-left my-2 md:mb-0">
              Frustración {{ index +1 }}:
              <br>
          </label>

          <h4 class="mb-1 px-3">{{ f.frustracion }}</h4>

        </div>

      </div>
            
      <!-- Marcas -->
      <div class="w-full mt-4  bg-emerald-100 rounded-md">
        
        <h1 class="text-2xl  text-center font-bold  text-black">Marcas</h1>
        
        <!-- recorro array de frustraciones y llamo a index -->
        <div class="w-full mt-4 mx-auto px-3" v-for="m,index in buscados.marcas">

          <label class=" text-black font-bold md:text-left my-2 md:mb-0">
              Marca {{ index +1 }}:
              <br>
          </label>

          <h4 class="mb-1 px-3">{{ m.marca }}</h4>

        </div>

      </div>

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
  <div class="grid grid-cols-2 mx-auto p-1 border-4 rounded-lg bg-black  border-red-50 ">

    <h1 class="text-center text-white text-4xl font-bold my-4"> Lista de Personas</h1><br>
    
    <div class="text-2xl text-black mx-auto border-4 border-separate" >
        
        <table class = "table border-black border-4 text-base mx-auto">
          <thead >
            <tr class="border-black border-4 bg-emerald-500">
              <th class="border-black border-4">Id</th>
              <th class="border-black border-4">Nombre</th>
              <th class="border-black border-4">Edad</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(p, index) in personas"  class=" border-black border-4">
              <td class=" border-black border-2 mx-3  bg-white py-2 px-2 ">  {{ index += 1 }} </td>
              <td class=" border-black border-2 mx-2  bg-white py-2 px-2">{{ p.nombre }}</td>
              <td class=" border-black border-2 mx-2  bg-white py-2 px-2">{{ p.edad }}</td>
              <td class=" border-black border-2 mx-2  bg-white py-2 px-2"> <button @click="InfoPer(p.id)"> VER PERSONA </button> </td>
            </tr>
            
          </tbody>
        </table>

    </div>

    <!--Informacion sólo Uno-->
    <div class=" py-15"  v-if="mostrarUno">
      
      <!--carta de personaje-->          
      <div class="w-3/4 mx-auto px-5 my-16 border-4 border-indigo-50  bg-white rounded-sm">

        <!-- Información personal -->
        <div class="w-full mt-4 bg-lime-100  rounded-md">
          <h1 class="text-2xl  text-center font-bold  text-black">Información personal</h1>
      
          <h2 class="mb-1 px-3"> <b>Id: </b> {{ infoUno.id }}</h2>
          <h2 class="mb-1 px-3"> <b>Nombre:</b> {{ infoUno.nombre }}</h2>
          <h4 class="mb-1 px-3"> <b>Especie:</b> {{ infoUno.edad}}</h4>
          <h4 class="mb-1 px-3"> <b>Estado Civil:</b> {{ infoUno.estadoCivil}}</h4>
          <h4 class="mb-1 px-3"> <b>Tipo:</b> {{ infoUno.trabajo }}</h4>
          <h4 class="mb-1 px-3"> <b>Locación:</b> {{ infoUno.residencia}}</h4>
        </div>

        <!-- Cita -->
        <div class="w-full mt-4 bg-orange-100 rounded-md">
          <h1 class="text-2xl  text-center font-bold  text-black">Frase</h1>
          <h4 class="mb-1 px-3"> <b>Cita:</b> <br> {{ infoUno.cita}}</h4>
          <h4 class="mb-1 px-3"> <b>Autor:</b> {{ infoUno.citaAutor}}</h4>
          
        </div>

        
        <!-- Personal -->
        <div class="w-full mt-4  bg-indigo-100 rounded-md">
          
          <h1 class="text-2xl  text-center font-bold  text-black">Biografía</h1>
            
          <h4 class="mb-1 px-3"> <b>Yo:</b> <br>{{ infoUno.bio}}</h4>
        </div>

        <!-- Personalidades-->
        <div class="w-full mt-4 bg-fuchsia-200 rounded-md ">
          <h1 class="text-2xl  text-center font-bold  text-black">Personalidades</h1>

          <div class="w-full mt-4 mx-auto px-3 ">
            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                "Mente"  
                <br>
            </label>

            <div class="flex  justify-between px-4">
              <label class="text-black  text-left md:text-left my-2 md:mb-0">
                Extrovertido: <br>  {{infoUno.personalidad01 }}%
              </label>
              
              <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
                Introvertido: <br> {{ 100 - infoUno.personalidad01}}%
              </label>
            </div>

            <div class=" px-4">
            <input type="range" v-model="infoUno.personalidad01" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
            </div>

          </div>

          <div class="w-full mt-4 mx-auto px-3">
              <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                  "Energia"  
                  <br>
              </label>

              <div class="flex  justify-between px-4">
                <label class="text-black  text-left md:text-left my-2 md:mb-0">
                  Intuitivo: <br>  {{infoUno.personalidad02 }}%
                </label>
                
                <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
                  Observador: <br> {{ 100 - infoUno.personalidad02}}%
                </label>
              </div>
              <div class=" px-4">
              <input type="range" v-model="infoUno.personalidad02" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
              </div>

          </div>

          <div class="w-full mt-4 mx-auto px-3">
            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                "Naturaleza"  
                <br>
            </label>

            <div class="flex  justify-between px-4">
              <label class="text-black  text-left md:text-left my-2 md:mb-0">
                Pensamiento: <br>  {{infoUno.personalidad03 }}%
              </label>
              
              <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
                Emocional: <br> {{ 100 - infoUno.personalidad03}}%
              </label>
            </div>
            <div class=" px-3">
            <input type="range" v-model="infoUno.personalidad03" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
            </div>

          </div>

          <div class="w-full mt-4 mx-auto px-3">
            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                "Identidad"  
                <br>
            </label>

            <div class="flex  justify-between px-3">
              <label class="text-black  text-left md:text-left my-2 md:mb-0">
                Asertivo: <br>  {{infoUno.personalidad04 }}%
              </label>
              
              <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
                Cauteloso: <br> {{ 100 - infoUno.personalidad04}}%
              </label>
            </div>
            <div class=" px-3">
            <input type="range" v-model="infoUno.personalidad04" class="w-full -3 py-3 mx-auto rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="porcentaje" placeholder="" typeof="slider" min="0" max="100"/>
            </div>

          </div>
        </div>

        <!-- Objetivos -->
        <div class="w-full mt-4  bg-yellow-100 rounded-md">
          
          <h1 class="text-2xl  text-center font-bold  text-black">Objetivos</h1>
          
          <!-- recorro array de objetivos y llamo a index -->
          <div class="w-full mt-4 mx-auto px-3" v-for="o,index in infoUno.objetivos">

            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                Objetivo {{ index +1 }}:
                <br>
            </label>

            <h4 class="mb-1 px-3">{{ o.objetivo }}</h4>

          </div>

        </div>

        <!-- Frustraciones -->
        <div class="w-full mt-4  bg-red-100 rounded-md">
          
          <h1 class="text-2xl  text-center font-bold  text-black">Frustracionees</h1>
          
          <!-- recorro array de frustraciones y llamo a index -->
          <div class="w-full mt-4 mx-auto px-3" v-for="f,index in infoUno.frustraciones">

            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                Frustración {{ index +1 }}:
                <br>
            </label>

            <h4 class="mb-1 px-3">{{ f.frustracion }}</h4>

          </div>

        </div>
               
        <!-- Marcas -->
        <div class="w-full mt-4  bg-emerald-100  rounded-md">
          
          <h1 class="text-2xl  text-center font-bold  text-black">Marcas</h1>
          
          <!-- recorro array de frustraciones y llamo a index -->
          <div class="w-full mt-4 mx-auto px-3" v-for="m,index in infoUno.marcas">

            <label class=" text-black font-bold md:text-left my-2 md:mb-0">
                Marca {{ index +1 }}:
                <br>
            </label>

            <h4 class="mb-1 px-3">{{ m.marca }}</h4>

          </div>

        </div>

      </div>

    </div>
        
  </div>

 
</template>