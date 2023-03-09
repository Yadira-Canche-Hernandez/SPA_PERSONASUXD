<script>
//importación de componentes
import BotonEnviar from '../components/BotonEnviar.vue';
import InputText from '../components/InputText.vue';
import TextArea from '../components/TextArea.vue';
import InputSlider from '../components/InputSlider.vue';

import axios from 'axios';



export default {
  components:{
    //nombre con el que se llama a los componentes
    BotonEnviar, InputText, TextArea, InputSlider
  },
  
  emits: ['dataIT, dataTA, porcentaje'],

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

        //Funciones para pasar los datos que recibe como componentes a las variables declaradas
        
        //Nombre
        DataIT1(t){
          //le asignamos lo que recibe a la variable
          this.Nombre=t
        },

        //Edad
        DataIT2(t){
          //le asignamos lo que recibe a la variable
          this.Edad=t
        },

        //Trabajo
        DataIT3(t){
          //le asignamos lo que recibe a la variable
          this.Trabajo=t
        },

        //Residencia
        DataIT4(t){
          //le asignamos lo que recibe a la variable
          this.Residencia=t
        },

        //Cita
        TextAreaC(a){
          //le asignamos lo que recibe a la variable
          this.Cita=a
        },

        //Biografia
        TextAreaB(a){
          //le asignamos lo que recibe a la variable
          this.Bio=a
        },

        //Personalidades
        SliderP1(s){
          this.Personalidad1=s
        },

        SliderP2(s){
          this.Personalidad2=s
        },

        SliderP3(s){
          this.Personalidad3=s
        },

        SliderP4(s){
          this.Personalidad4=s
        },

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
    
    <div class="w-3/5 m-w-450 m-auto h-auto rounded-lg bg-white py-8 px-7 mb-5">
      
      <h1 class="text-4xl font-bold text-black text-center">Registro</h1>

      <form class="w-full mt-6">
        
        <div class="grid grid-cols-2">

          <div class=" bg-rose-200  p-3 rounded-lg">
            <div class="w-full">
              <h1 class="text-2xl  text-center font-bold  text-black ">Datos personales</h1>
              
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Nombre
              </label>
              
              <!--Uso al componente-->
              <InputText @dataIT="DataIT1" > </InputText>
            
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0" >
                Edad
              </label>
              
              <!--Uso al componente-->
              <InputText @dataIT= "DataIT2" > </InputText>

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
              
              <!--Uso al componente-->
              <InputText @dataIT= "DataIT3" > </InputText>
            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Residencia
              </label>
              
              <!--Uso al componente-->
              <InputText @dataIT= "DataIT4"> </InputText>

            </div>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                Escribe una cita o frase de libros, peliculas, etc. con la que te identificas
              </label>
              
              <!--Uso al componente-->
              <TextArea @dataTA = "TextAreaC"></TextArea>
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
              
              <!--Uso al componente-->
              <TextArea @dataTA = "TextAreaB"></TextArea>

            </div>
          </div>

          <div class="ml-5 bg-rose-200  p-3 rounded-lg w-full ">

            <h1 class="text-2xl  text-center font-bold  text-black">Datos persona UXD</h1>

            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                "Mente"  
                <br>
              </label>

              <div class="flex justify-between px-3  ">
                <label class="text-black  text-left md:text-left my-2 md:mb-0">
                  Extrovertido: <br>  {{ this.Personalidad1 }}%
                </label>
                
                <label class="text-black  text-end  mr-0 md:text-right my-2 md:mb-0">
                  Introvertido: <br> {{ 100 - this.Personalidad1 }}%
                </label>

              </div>

              <!--Uso al componente-->
              <InputSlider @porcentaje="SliderP1" ></InputSlider>
            
          </div>
            
            <div class="w-full mt-4">

              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                "Energia" 
              </label>

              <div class="flex justify-between px-3  ">
                <label class="text-black text-left md:text-left my-2 md:mb-0">
                  Intuitivo: <br>  {{ this.Personalidad2 }}%
                </label>
                
                <label class="text-black text-end  mr-0 md:text-right my-2 md:mb-0">
                  Observador: <br> {{ 100 - this.Personalidad2 }}%
                </label>

              </div>

              <!--Uso al componente-->
              <InputSlider @porcentaje="SliderP2" ></InputSlider>
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                "Naturaleza"
              </label>

              <div class="flex justify-between px-3  ">
                <label class="text-black text-left md:text-left my-2 md:mb-0">
                  Pensamiento: <br>  {{ this.Personalidad3 }}%
                </label>
                
                <label class="text-black text-end  mr-0 md:text-right my-2 md:mb-0">
                  Emocional: <br> {{ 100 - this.Personalidad3 }}%
                </label>

              </div>

              <!--Uso al componente-->
              <InputSlider @porcentaje="SliderP3" ></InputSlider>
              
            </div>
            
            <div class="w-full mt-4">
              <label class="block text-black font-bold md:text-left my-2 md:mb-0">
                "Identidad"
              </label>

              <div class="flex justify-between px-3  ">
                <label class="text-black text-left md:text-left my-2 md:mb-0">
                  Asertivo: <br>  {{ this.Personalidad4 }}%
                </label>
                
                <label class="text-black text-end  mr-0 md:text-right my-2 md:mb-0">
                  Cauteloso: <br> {{ 100 - this.Personalidad4 }}%
                </label>

              </div>

              <!--Uso al componente-->
              <InputSlider @porcentaje="SliderP4" ></InputSlider>
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
                        
            <BotonEnviar @click="Registro()" >
              Enviar
            </BotonEnviar>

        

      </form> 
    </div>
    
  </div>  
  
</template>