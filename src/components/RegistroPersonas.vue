<script>
import axios from 'axios';


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
          Personalidad1: "50",
          Personalidad2: "50",
          Personalidad3: "50",
          Personalidad4: "50",
          Objetivos: [],
          Frustraciones: [],
          Motivaciones: [],
          Marcas: "",

          //variable validaciones
          validar:false
        };
    },
    mounted() {
    },
    methods: {

        //Función para enviar informacion de una persona
        Registro() {
          if(this.Validar()){
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
            console.log(response.status);
            });
          }
            
        },

        Validar(){
          //nombre
          if(this.Nombre != "" && !isNaN (this.Nombre) === false && this.Nombre.length <201 && this.Nombre.length > 2 ) {
            console.log("el nombre es correcto")
             
            //edad
            if (this.Edad.length < 3 && this.Edad != ""){
              console.log("edad existe")
            }else{
              console.log("no existe esa edad")
            }

            //Estado civil
            if (this.EstadoCivil != ""){
              console.log("si selecciono estado civil")
            }else{
              console.log("no selecciono estado civil")
              return false
            }

            //Trabajo
            if (this.Trabajo.length < 201 && this.Trabajo != "" && !isNaN (this.Trabajo) === false){
              console.log("trabajo existe")
            }else{
              console.log("no existe trabajo")
              return false
            }

            //Residencia
            if (this.Residencia.length < 201 && this.Residencia != "" && !isNaN (this.Residencia) === false){
              console.log("residencia existe")
            }else{
              console.log("no existe residencia")
              return false
            }

            //Cita
            if (this.Cita.length < 501 && this.Cita != "" && !isNaN (this.Cita) === false){
              console.log("Cita existe")
            }else{
              console.log("Cita no existe")
              return false
            }

            //CitaAutor
            if (this.CitaAutor.length < 501 && this.CitaAutor != "" && !isNaN (this.CitaAutor) === false){
              console.log("CitaAutor existe")
            }else{
              console.log("CitaAutor no existe")
              return false
            }

            //Bio
            if (this.Bio.length < 701 && this.Bio != "" && !isNaN (this.CitaAutor) === false){
              console.log("Bio correcta")
            }else{
              console.log("Bio incorrecta")
              return false
            }

          return true
                       
          }
          else{
            console.log("No pude registrarlo")
            return false
          }
          
        }
    },
    
}


</script>

<template class="flex mx-auto">

<div class="w-full h-full bg-gradient-to-r from-purple-600 via-blue-400 to-green-200 flex justify-item-center">
    
    <div class="w-2/4 m-w-450 m-auto h-auto rounded-lg bg-white py-8 px-7 mb-5">
      
      <h1 class="text-4xl font-bold text-black text-center">Registro</h1>

      <form class="w-full mt-6">
        
        <div class="grid grid-cols-2">

          <div class="bg-rose-200  p-3 rounded-lg">
            <div class="w-full">
              <h1 class="text-2xl  text-center font-bold  text-black ">Datos personales</h1>
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Nombre
              </label>
              <input type="text" v-model="Nombre" class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none" id="nombre" placeholder="Nombre"/>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0" >
                Edad
              </label>
              <input type="text" v-model="Edad" class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none" id="edad" placeholder=""/>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Estado Civil
              </label>
              <select v-model="EstadoCivil" name="EstadoCivil" id="EstadoCivil"  class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none">
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
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Trabajo
              </label>
              <input type="text" v-model="Trabajo" class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none" id="trabajo" placeholder=""/>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Residencia
              </label>
              <input type="text" v-model="Residencia" class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none" id="Residencia" placeholder=""/>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Escribe una cita o frase de libros, peliculas, etc. con la que te identificas
              </label>
              <input type="text" v-model="Cita" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Cita" placeholder=""/>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Nombre del autor de la cita o frase anterior
              </label>
              <input type="text" v-model="CitaAutor" class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none" id="CitaAutor" placeholder=""/>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Biografía
              </label>
              <textarea type="text" v-model="Bio" class="w-full py-2.5 px-4 rounded-lg bg-gray-50 focus:shadow focus:bg-white focus:outline-none" id="Bio" placeholder="">
              </textarea>
            </div>
          </div>

          <div class="ml-5 bg-rose-200  p-3 rounded-lg ">

            <h1 class="text-2xl  text-center font-bold  text-black">Datos persona UXD</h1>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Personalidad 1  
                <br>
                  {{ this.Personalidad1 }}%
              </label>
              <input type="range" v-model="Personalidad1" class="w-full px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad1" placeholder="" typeof="slider" min="0" max="100"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Personalidad 2 
                <br>{{ this.Personalidad2 }}%
              </label>
              <input type="range" v-model="Personalidad2" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad2" placeholder="" typeof="slider" min="0" max="100"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Personalidad 3
                <br>
                {{ this.Personalidad3 }}%
              </label>
              <input type="range" v-model="Personalidad3" class="w-full py-3 px-5 rounded-lg transition-colors bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad3" placeholder="" typeof="slider" min="0" max="100"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Personalidad 4
                <br>
                {{ this.Personalidad4 }}%    
              </label>
              <input type="range" v-model="Personalidad4" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Personalidad4" placeholder="" typeof="slider" min="0" max="100"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Objetivos
              </label>
              <input type="text" v-model="Objetivos" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Objetivos"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Frustraciones   
              </label>
              <input type="text" v-model="Frustraciones" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Frustraciones"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Motivaciones  
              </label>
              <input type="text" v-model="Motivaciones" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Motivaciones"/>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Marcas  
              </label>
              <input type="text" v-model="Marcas" class="w-full py-2.5 px-4 rounded-lg bg-gray-100 focus:shadow focus:bg-white focus:outline-none" id="Marcas" placeholder="Separa por comas"/>
            </div>
          </div>
          
        </div>

          <!--Boton Registrar-->
          <div class="flex justify-center items-center space-x-4 text-base my-8">
              
              <button @click="Registro()" class="h-14 mx-2 sm:h-10 px-7 font-semibold rounded-md bg-slate-800 text-white my-2 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105" type="button">Enviar </button>
          </div>

        

      </form> 
    </div>
    
  </div>  
  
</template>