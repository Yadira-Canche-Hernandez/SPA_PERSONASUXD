<script>
import axios from 'axios'



export default {

  data() {
    return {

      //variables que va recibir
      Nombre: " ",
      Edad: " ",
      EstadoCivil: " ",
      Trabajo:" ",
      Residencia: " ",
      Cita: " ",
      CitaAutor: " ",
      Bio: " ",
      Personalidad1: " ",
      Personalidad2:" ",
      Personalidad3: " ",
      Personalidad4: " ",
      Objetivos: " ",
      Frustraciones: [],
      Motivaciones: [],
      Marcas: " "
      
    }
  },

  mounted() {
  },

  methods: {
    
    //informacion de una persona
    Registro( ) {  
      axios
        .post("/api/guardarPersonasUxd.php", {
        nombre: this.nombre,
        objetivos:this.objetivos,
        frustraciones: this.frustraciones,
        motivaciones: this.motivaciones,
        marcas: this.marcas,
        //completar las variables, estas deben llamarse como las que se recibirán en el backend sin el símbolo del dolar $
        })
        .then((response) => {
        console.log(response.status)
        });
      
    }
  },
}

</script>

<template class="flex mx-auto">

  
</template>