<script>
import axios from 'axios'
import { getTransitionRawChildren } from 'vue';



export default {

  data() {
    return {

      //variables que va recibir
      Nombre: "",
      Edad: "",
      EstadoCivil: "",
      Trabajo: "",
      Residencia: "",
      Cita: "",
      CitaAutor: "",
      Bio: "",
      Personalidad1: "",
      Personalidad2: "",
      Personalidad3: "",
      Personalidad4: "",
      Objetivos: "",
      Frustraciones: [],
      Motivaciones: [],
      Marcas: "",

    }
  },

  mounted() {
  },

  methods: {
    
    //Función para enviar informacion de una persona
    Registro() {  
      axios
        .post("/api/guardarPersonasUxd.php", {

          //declaracion de variables del backend
          nombre: this.Nombre,
          edad: this.Edad,
          estadoCivil: this.EstadoCivil,
          trabajo: this.Trabajo,
          residencia: this.Residencia,
          cita: this.Cita,
          citaAutor: this.CitaAutor,
          bio: this.Bio,
          personalidad01: this.Personalidad1,
          personalidad02: this.Personalidad2,
          personalidad03: this.Personalidad3,
          personalidad04: this.Personalidad4,
          objetivos: this.Objetivos,
          frustraciones: this.Frustraciones,
          motivaciones: this.Motivaciones,
          marcas: this.Marcas
        
        })
        .then((response) => {
        //comprobación de envio a la base de datos con numero 200
        console.log(response.status)
        });
      
    }
  },
}

</script>

<template class="flex mx-auto">

  <div class="w-full h-screen bg-gradient-to-r from-purple-600 via-blue-400 to-green-200 flex justify-item-center">
    
    <div class="w-2/4 m-w-450 m-auto h-auto rounded-lg bg-white py-8 px-7">
      
      <h1 class="text-4xl font-bold text-gray-600 text-center">Registro</h1>

      <form class="w-full mt-6" method="get">

        <div class="w-full">
          <label class="block text-black font-bold md:text-left my-2 md:mb-0">
            Nombre
          </label>
          <input type="text" v-model="Nombre" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="nombre" placeholder="Nombre"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0" >
            Edad
          </label>
          <input type="text" v-model="Edad" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="edad" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Estado Civil
          </label>
          <select v-model="selected" name="EstadoCivil" id="EstadoCivil"  class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none">
            <option disabled value="">Selecciona </option>
            <option value="1">Soltero</option>
            <option value="2">Casado </option>
            <option value="3">Divorciado</option>
            <option value="4">Separado</option>
            <option value="5">Unión libre</option>
            <option value="6">Viudo</option>
          </select>
          
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Trabajo
          </label>
          <input type="text" v-model="Trabajo" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="trabajo" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Residencia
          </label>
          <input type="text" v-model="Residencia" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Residencia" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Cita
          </label>
          <input type="text" v-model="Cita" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Cita" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Cita Autor
          </label>
          <input type="text" v-model="CitaAutor" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="CitaAutor" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Biografia
          </label>
          <input type="text" v-model="Bio" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Bio" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Personalidad 1  
          </label>
          <input type="range" v-model="Personalidad1" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad1" placeholder="" typeof="slider" min="0" max="100"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Personalidad 2 
          </label>
          <input type="range" v-model="Personalidad2" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad2" placeholder="" typeof="slider" min="0" max="100"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
             Personalidad 3 
          </label>
          <input type="range" v-model="Personalidad3" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad3" placeholder="" typeof="slider" min="0" max="100"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Personalidad 4    
          </label>
          <input type="range" v-model="Personalidad4" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad4" placeholder="" typeof="slider" min="0" max="100"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Objetivos
          </label>
          <input type="text" v-model="Objetivos" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Objetivos" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Frustraciones   
          </label>
          <input type="text" v-model="Frustraciones" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Frustraciones" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Motivaciones  
          </label>
          <input type="text" v-model="Motivaciones" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Motivaciones" placeholder=""/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0">
            Marcas  
          </label>
          <input type="text" v-model="Marcas" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Marcas" placeholder=""/>
        </div>

        <!--Botones paginas-->
        <div  class="flex justify-center items-center space-x-4 text-base my-8">
            <!--Pagina anterior-->
            <button @click="Registro()" class="h-14 mx-2 sm:h-10 px-7 font-semibold rounded-md bg-slate-800 text-white my-2 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105" type="submit">Enviar </button>
        </div>

      </form> 

    </div>

  </div>
  
</template>