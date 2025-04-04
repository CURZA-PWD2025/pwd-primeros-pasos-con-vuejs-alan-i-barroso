<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const nombreUsuario = ref ("")
const email = ref ("")
const contraseña = ref ("")
const añoNacimiento = ref ()

const usuario = ref ({})

function calcularEdad(fechaNacimiento: string): number{
  const nacimiento= new Date(fechaNacimiento) 
  const hoy =new Date() //en hoy se guarda la fecha actual
  let edad = hoy.getFullYear() - nacimiento.getFullYear() //restamos año actual - fecha nacimiento
  const mes = hoy.getMonth() - nacimiento.getMonth() // restamos los meses ya que con .getMonth los meses se guardan en numeros
  // si el mes actual es menor o es el mismo mes pero el dia actual es menor restamos 1 a la edad
  if (mes <0 || mes == 0 && hoy.getDate()< nacimiento.getDate()) {
    edad--
  }
  return edad
}

function manejoForm() {
  if (nombreUsuario.value && email.value && contraseña.value && añoNacimiento.value){
    const edad = calcularEdad(añoNacimiento.value)
    let usuario = {
      nombreUsuario: nombreUsuario.value,
      email: email.value,
      contraseña: contraseña.value,
      añoNacimiento: añoNacimiento.value,
      edad: edad
    }
    nombreUsuario.value = ""
    email.value= ""
    contraseña.value = ""
    añoNacimiento.value = ""
    alert ("usuario: " + usuario.nombreUsuario + " edad: " + usuario.edad + " email: " + usuario.email + " datos ingresados correctamente")
    console.log("datos guardados: ", usuario)
  }
  else {
    alert("debe llenar los componentes correctamente")
  }
}
</script>

<template>
  <h3>hola</h3>
  <h2>{{ msg }}</h2>
  <form @submit.prevent="manejoForm">
    <input type="text" placeholder="nombre de usuario" maxlength="15" v-model="nombreUsuario">
    <br>
    <input type="email" placeholder="email" v-model="email">
    <br>
    <input type="password" placeholder="contraseña" v-model="contraseña">
    <br>
    <input type="date" placeholder="año nacimiento" v-model="añoNacimiento">
    <br>
    <input type="submit" value="enviar datos">
  </form>
  
  <div>usuario: {{ nombreUsuario }} <br> email: {{ email }} <br> edad:<!-- {{ edad }} arreglar el porque no funciona --> </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
h2 {
  font-size: 2em;
  color: #333;
  text-align: center;
  margin-bottom: 20px;
  font-weight: 600;
  border-bottom: 2px solid #ddd;
  padding-bottom: 10px;
}
form{
  background-color: #ffffff;
  max-width: 400px;
  margin: 50px auto;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}
form input[type="text"],
form input[type="email"],
form input[type="password"],
form input[type="date"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  transition: border 0.3s ease;
}
form input[type="submit"] {
  background-color: #007bff;
  border: none;
  color: #fff;
  padding: 12px;
  font-size: 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  width: 100%;
}
form input[type="submit"]:hover,
form button:hover {
  background-color: #0056b3;
}
div{
  margin-top: 20px;                 
  padding: 15px;                    
  background-color: #ffffff;         
  border: 1px solid #ddd;           
  border-radius: 8px;                
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);  
  font-size: 1rem;                   
  color: #444;                   
  line-height: 1.6;                 
  max-width: 600px;                 
  margin-left: auto;
  margin-right: auto;
  transition: box-shadow 0.3s ease;  
}

.read-the-docs {

  color: #888;
}
</style>
