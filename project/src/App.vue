<template>
  <div class="flex justify-center mt-10">
    <img src="./assets/1_facebook.jpg" alt="banner" class="w-96 h-52 rounded-full ">
  </div>
  <chooseMenu v-show="cMenu" @createList="goList" @forFile="goFile" />
  <div>
    <div v-show="howManyPerson">
      <howPerson @numberPerson=updatePerson />
      <div class="flex flex-row justify-center  mt-10">
        <button @click="addPerson"
          class=" bg-amber-700 hover:bg-amber-500 w-28 h-12 rounded text-white shadow-xl">Aceptar</button>
      </div>
    </div>
    <div v-show="seeFile">
      <readFile @load=loadFile />
    </div>
    <div class="flex flex-col items-center" v-show="introPerson">
      <introducePerson @createList=photoPerson :maxNumber=maxPerson @aceptSee=changeButtonSee />
    </div>
    <div class="flex justify-center" v-show="buttonSee">
      <button @click="pairing" class=" bg-red-500 w-28 h-12 rounded mt-10 hover:bg-red-200" :disabled="getPair">Obtener
        parejas</button>
    </div>
    <div v-show="detailPerson" class="mt-10 ml-10 flex flex-row gap-10 flex-wrap justify-center">
      <detailsPerson v-for="(el, key) in pairingPerson" :key="key" :name1="el[0].name" :name2="el[1].name"
        :photo1="el[0].photo" :photo2="el[1].photo" />
    </div>
    <div v-show="numeroCorrecto" class="mt-10 ml-10 flex flex-row gap-10 flex-wrap justify-center">
      <detailsPerson v-for="(el, key) in file" :key="key" :name1="el[0]" :name2="el[1]" :photo1="photo"
        :photo2="photo" />
    </div>
    <h1 v-show="numeroIncorrecto">Lista Impares</h1>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref, computed } from 'vue';
import howPerson from './components/howPerson.vue';
import introducePerson from "./components/introducePerson.vue";
import detailsPerson from "./components/detailsPerson.vue";
import readFile from "./components/readFile.vue";
import chooseMenu from "./components/chooseMenu.vue"

let maxPerson = ref();
let listPerson = ref([]);
let introPerson = ref();
let howManyPerson = ref(false);
let buttonSee = ref();
let detailPerson = ref(false);
let pairingPerson = ref([]);
let getPair = ref(true);
let seeFile = ref(false);
let file = ref([]);
let numeroIncorrecto = ref(false);
let numeroCorrecto = ref(false);
const cMenu = ref(true);
const photo = ref("https://randomuser.me/api/portraits/women/80.jpg");

const loadFile = (fil) => {

  let auxiliar = fil
    .toString()
    .trim()
    .split('\n')
  if (auxiliar.length % 2 == 0) {
    numeroCorrecto.value = true;
    file.value = auxiliar
      .sort(() => Math.random() - 0.5)
      .map((el, idx, arr) => (idx % 2 == 1) ? [el, arr[idx - 1]] : null)
      .filter(el => el !== null);
  } else {
    numeroIncorrecto.value = true;
    file.value = [];
  }

}

const goFile = () => { cMenu.value = false; seeFile.value = true }

const goList = () => { cMenu.value = false; howManyPerson.value = true }

const updatePerson = (number) => maxPerson.value = number;

const addPerson = () => { introPerson.value = true; howManyPerson.value = false };

const photoPerson = async (lista) => {
  let auxArray = [];

  try {
    for (let index = 0; index < lista.length; index++) {

      const res = await axios.get(`https://randomuser.me/api/?gender=${lista[index][1]}`);

      auxArray.push({ "name": lista[index][0], "photo": res.data.results[0].picture.large })
    }

    listPerson.value = auxArray;
  }
  catch (error) {
    console.log(error);
  }
  getPair.value = false;
}

const pairing = () => {

  let auxList = listPerson.value;
  //intentar resetear parejas!!!!!!!!!!!!!!!!!!!!!!!
  for (let i = 0; i < listPerson.value.length; i = i + 2) {

    let seleccion1 = auxList[Math.floor(Math.random() * auxList.length)];
    auxList = auxList.filter((el) => el.name != seleccion1.name);
    let seleccion2 = auxList[Math.floor(Math.random() * auxList.length)];
    auxList = auxList.filter((el) => el.name != seleccion2.name);
    pairingPerson.value.push([seleccion1, seleccion2]);

  }

  detailPerson.value = true;
  introPerson.value = false;
}

const changeButtonSee = (status) => buttonSee.value = status;

</script>
