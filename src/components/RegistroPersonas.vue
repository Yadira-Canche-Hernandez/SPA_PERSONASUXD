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

      valida: false

    }
  },

  mounted() {
  },

  methods: {
    /*ValidarNombre(){
      if(!isNaN (this.Nombre) === false && this.Nombre.length <201 && this.Nombre.length > 3 ) {
        valida = true
      }
      else{
        valida = false
      }
    }*/

    //Función para enviar informacion de una persona
    Registro() {  
      //if(this.validar== true){}
      if(!isNaN (this.Nombre) === false && this.Nombre.length <201 && this.Nombre.length > 3 ) {
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
      else{
      console.log("es numerico")
      console.log("es menor a 3")
      }
    },

  },
}

</script>

<template class="flex mx-auto">

  <div class="w-full h-screen bg-gradient-to-r from-purple-600 via-blue-400 to-green-200 flex justify-item-center">
    
    <div class="w-2/4 m-w-450 m-auto h-auto rounded-lg bg-white py-8 px-7">
      
      <h1 class="text-4xl font-bold text-gray-600 text-center">Registro</h1>

      <form class="w-full mt-6" method="get">

        <div class="w-full">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0" for="inline-full-name">
              Nombre
          </label>
          <input type="text" v-model="Nombre" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="inline-full-name" placeholder="Nombre"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0" for="edad">
              Edad
          </label>
          <input type="text" v-model="Edad" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="inline-full-name" placeholder="Nombre"/>
        </div>

        <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0" for="estado">
              Estado Civil
          </label>
          <input type="text" v-model="EstadoCivil" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="inline-full-name" placeholder="Soltero"/>
        </div>

                <div class="w-full mt-4">
          <label class="block text-gray-500 font-bold md:text-left my-2 md:mb-0" for="estado">
              Estado Civil
          </label>
          <input type="text" v-model="EstadoCivil" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="inline-full-name" placeholder="Soltero"/>
        </div>
        <!--Botones paginas-->
        <div @click="Registro()" class="flex justify-center items-center space-x-4 text-base my-8">
            <!--Pagina anterior-->
            <button  class="h-14 mx-2 sm:h-10 px-7 font-semibold rounded-md bg-slate-800 text-white my-2 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105" type="button">Enviar </button>
        </div>
      </form> 
    </div>
  </div>
  
</template>