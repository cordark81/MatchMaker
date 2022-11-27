<template>
  <div>
    <div v-show="howManyPerson">
      <howPerson @numberPerson=updatePerson />
      <div class="flex flex-col items-center mt-10">
        <button @click="addPerson" class=" bg-red-500 w-28 h-12 rounded">Aceptar</button>
      </div>
    </div>
    <div class="flex flex-col items-center" v-show="introPerson">
      <introducePerson @enterPerson="aceptPerson" :maxNumber=maxPerson @aceptSee=changeButtonSee @createList=photoPerson(listPerson) />
         </div>
    <div class="flex justify-center" v-show="buttonSee">
        <button @click="pairing(listPerson)" class=" bg-red-500 w-28 h-12 rounded mt-10">Obtener parejas</button>
      </div>
    <div v-show="detailPerson" class="mt-10 ml-10 flex flex-row gap-10 flex-wrap justify-center">
      <detailsPerson v-for="person in pairingPerson" :name1="person[0].name" :name2="person[1].name" :photo1="person[0].photo" :photo2="person[1].photo" />
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
let pairingPerson = ref([]);

const aceptPerson = (name, gender) => {
  listPerson.value.push([name, gender]);
};

const updatePerson = (number) => maxPerson.value = number;

const addPerson = () => { introPerson.value = true; howManyPerson.value = false };

const photoPerson = async (lista) => {
  let auxArray = [];
  try{
  for (let index = 0; index < listPerson.value.length; index++) {

    const res = await axios.get(`https://randomuser.me/api/?gender=${lista[index][1]}`);

    auxArray.push({ "name": lista[index][0], "photo": res.data.results[0].picture.large })
  }

  listPerson.value = auxArray;

  introPerson.value = false;

  }catch(error){
    console.log(error);
  }
  
}

const pairing = (list) => {

  let auxList = list;

  for (let i = 0; i < list.length; i=i+2) {
    let seleccion1 = auxList[Math.floor(Math.random() * auxList.length)];
    auxList = auxList.filter((el) => el.name != seleccion1.name);
    let seleccion2 = auxList[Math.floor(Math.random() * auxList.length)];
    auxList = auxList.filter((el) => el.name != seleccion2.name);
    pairingPerson.value.push([seleccion1,seleccion2]);
 
  }
  detailPerson.value = true;
}


const changeButtonSee = (status) => buttonSee.value = status;

</script>
