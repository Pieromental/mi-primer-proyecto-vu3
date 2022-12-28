<template>
  <div>
    <h1>{{name.toUpperCase()}}</h1>
    <h2 :style="styleColor"  >Soy Azul</h2>
    <!-- <h2 :style="`color:${arrayColors[2]}`"  >Soy Peru</h2> -->
    <!-- <h1 v-for="(color, index) in arrayColors" :key="index">{{index}} - {{color.name}} : {{ color.price }} ({{color.descripcion }})</h1> -->
    <template v-for="(color, index) in arrayColors" :key="index">
      <li v-if="color.stock >5">{{index}} - {{color.name}} : {{ color.price }} ({{color.descripcion }})</li>
    </template>
    <h3>{{activo? "Estoy activo" : "Estoy inactivo"}}</h3>
    <div>
     <ul v-if="activo">
       <li>Piero Salazar</li>
       <li>Alex Salazar</li>
     </ul>
     <p v-else-if="!activo">No muestro la lista - Pon variable activo en true si quieres ver XD</p>
     <p v-else>Wey Defineme ps</p>
     <h3 v-show="activo">Estoy activisimo v-show</h3>
    </div>
    <div class="container text-center">
      <div class="btn-group">
        <button @click="aumenta" class="btn btn-success">Aumenta</button>
        <button @click="disminuye" class="btn btn-danger">Disminuye</button>
        <button @click="resetea" class="btn btn-secondary">Resetea</button>
        <button @click="agregar" :disabled="active" class="btn btn-primary">Agregar</button>
      </div>
      <!-- <h3 :class="count > 0 ? 'positive':'negative'">{{ count }}</h3> -->
      <h3 :class="classCounter">{{ count }}</h3>
    </div>
    <div>
      <ul class="list-group">
        <li v-for="(num,index) of arrayNumbers" :key="index" class="list-group-item">
        {{ num }}
        </li>
      </ul>
    </div>
  </div>
  
</template>
<script setup>
import { ref,computed } from 'vue';
 const name="Vue Dinamico"
 const styleColor="color:blue"
 let arrayNumbers=ref([])
 const arrayColors=[
    {
      name:"Red",
      price:"S/1",
      descripcion:"Un color Rojo",
      stock:5
    },
    {
      name:"Blue",
      price:"S/2",
      descripcion:"Un color Azul",
      stock:10
    },
    {
      name:"Yellow",
      price:"S/3",
      descripcion:"Un color Amarillo",
      stock:15
    }
]
const activo=false
let count= ref(0);
const aumenta = () =>{
  console.log("Me diste Click y Aumente")
  count.value++;
  console.log(count);
 }
const disminuye = () =>{
  console.log("Me diste Click y Disminui")
  count.value--;
  console.log(count);
 }
const resetea = () =>{
  console.log("Me diste Click y Resetee")
  count.value=0;
  console.log(count);
 }
const agregar = () =>{
  arrayNumbers.value.push(count.value)
 }

 const classCounter= computed(()=>{
  if(count.value===0){
    return 'zero'
  }
  if(count.value>0){
    return 'positive'
  }
  if(count.value<0){
    return 'negative'
  }
 })
 const active= computed(()=>{
  const numSearch= arrayNumbers.value.find(num => num=== count.value)
  if(numSearch===0) return true
  return numSearch ? true : false;
 })
</script>
<style>
  h1{
    color: red;
  }
  .positive{
    color:green;
  }
  .negative{
    color: red;
  }
  .zero{
    color:peru;
  }
  
</style>