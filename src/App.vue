<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Titulo from "./components/Titulo.vue";
</script>

<template class="flex-col justify-center bg-blue-100 w-full h-full p-2">

<div class="w-full bg-purple-100 justify-items-center">
      
      <header>
  
        <nav class ="py-3 bg-black flex justify-self-center items-center text-white pl-5 gap-5 font-semibold hover:text-gray-500">
          <RouterLink to="/">Inicio</RouterLink>
          <RouterLink to="/RegistroPersonas">Registro de Personas</RouterLink>
          
        </nav>
        
        <div class="w-full">
  
          <Titulo msg="Creando personas UXD" />
  
          
        </div>
  
      </header>
  
  
    <RouterView />
  </div>
  </template>