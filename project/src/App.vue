<template>
  <div>
    <howPerson @numberPerson=updatePerson />
    <div class="flex flex-col items-center mt-10">
      <button @click="" class=" bg-red-500 w-28 h-12 rounded">Aceptar</button>
      <div class="flex " v-show="true">
        <introducePerson :number="2" @enterPerson="aceptPerson"/>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import howPerson from './components/howPerson.vue';
import introducePerson from "./components/introducePerson.vue";

let numberPerson = ref();
let Person = ref([]);

const aceptPerson = (name) =>{
  Person.value.push(name);
};

const updatePerson = (number) => { numberPerson.value = number };







</script>
