<template>
  <div>
    <div v-show="howManyPerson">
      <howPerson @numberPerson=updatePerson />
      <div class="flex flex-col items-center mt-10">
        <button @click="addPerson" class=" bg-red-500 w-28 h-12 rounded">Aceptar</button>
      </div>
    </div>
    <div class="flex flex-col items-center" v-show="introPerson">
      <introducePerson @enterPerson="aceptPerson" :maxNumber=maxPerson @aceptSee=changeButtonSee />
      <div v-show="buttonSee">
        <button @click="photoPerson(listPerson)" class=" bg-red-500 w-28 h-12 rounded mt-10">ver</button>
      </div>
    </div>
    <div v-show="detailPerson" class="mt-10 ml-10 flex flex-row gap-10 flex-wrap justify-center" >
      <detailsPerson v-for="person in listPerson" :key="person.name" :name=person.name :photo=person.photo />
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from 'vue';
import howPerson from './components/howPerson.vue';
import introducePerson from "./components/introducePerson.vue";
import detailsPerson from "./components/detailsPerson.vue";

let maxPerson = ref();
let listPerson = ref([]);
let introPerson = ref();
let howManyPerson = ref(true);
let buttonSee = ref();
let detailPerson = ref(false);

const aceptPerson = (name,gender) => {

  listPerson.value.push([name,gender]);
  

};

const updatePerson = (number) => maxPerson.value = number;

const addPerson = () => { introPerson.value = true; howManyPerson.value = false };

const photoPerson = async (lista) => {
  let auxArray=[];
  
  for (let index = 0; index < listPerson.value.length; index++) {
    
    const res = await axios.get(`https://randomuser.me/api/?gender=${lista[index][1]}`);  
    
    auxArray.push({"name": lista[index][0], "photo": res.data.results[0].picture.large})
  }
  
  listPerson.value=auxArray;

  introPerson.value = false;
  detailPerson.value = true;

}
const joinPersonPhoto = (lista, response) => {

  listPerson.value = lista.map((el, index) => { return { "name": el, "photo": response.results[index].picture.large } });
  
};

const changeButtonSee = (status) => buttonSee.value = status;

</script>
