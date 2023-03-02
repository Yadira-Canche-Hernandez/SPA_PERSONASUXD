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
    
    //Función para enviar informacion de una persona
    Registro( ) {  
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
        console.log(response.status)
        });
      
    }
  },
}

</script>

<template class="flex mx-auto">

  
</template>