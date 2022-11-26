<template>
  <div>
    <div v-show="howManyPerson">
      <howPerson @numberPerson=updatePerson />
      <div class="flex flex-col items-center mt-10">
        <button @click="addPerson" class=" bg-red-500 w-28 h-12 rounded">Aceptar</button>
      </div>
    </div>
    <div class="flex flex-col" v-show="introPerson">
      <introducePerson @enterPerson="aceptPerson" :maxNumber=maxPerson />
    </div>
    <button @click="photoPerson(listPerson)" class=" bg-red-500 w-28 h-12 rounded">prueba</button>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from 'vue';
import howPerson from './components/howPerson.vue';
import introducePerson from "./components/introducePerson.vue";

let maxPerson = ref();
let listPerson = ref([]);
let introPerson = ref();
let howManyPerson = ref(true);

const aceptPerson = (name) => {

  listPerson.value.push(name);

};

const updatePerson = (number) => maxPerson.value = number;

const addPerson = () => { introPerson.value = true; howManyPerson.value = false };

const photoPerson = async (lista) => {
  const res = await axios.get(`https://randomuser.me/api/?results=${lista.length}`);
  
  joinPersonPhoto(lista, res.data);


}
const joinPersonPhoto = (lista, response) => {

  lista=lista.map((el,index)=>{return{"name": el,"photo":response.results[index].picture.large}});




};




</script>
