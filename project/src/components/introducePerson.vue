<template>
    <div class="flex flex-col justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96">
            <div class="flex flex-col text-xl text-blue-700 items-center">
                <label for="name">Introduzca persona {{ contador }}</label>
                <input ref="bar" v-model="enter" @keyup.enter=checkName(enter,radioButton) type="text" name="name"
                    class="rounded border mb-2 border-blue-700 w-36 text-center" :disabled="stopEnter">

                <div class="flex items-baseline">
                    <label for="uno">Mujer</label>
                    <input class="ml-2" type="radio" id="uno" value="female" name="gender" v-model="radioButton"
                        :checked="resetCheckFemale" :disabled="stopEnter">
                    <label class="ml-5" for="Dos">Hombre</label>
                    <input class="ml-2" type="radio" id="Dos" value="male" name="gender" v-model="radioButton"
                        :checked="resetCheckMale" :disabled="stopEnter">
                </div>

            </div>
        </div>
        <div v-show="warning" class="border-2 border-red-600 mt-10 rounded-full">
            <h1 class="text-xl text-white text-center text-red-600">El nombre "{{ lastName }}" esta repetido</h1>
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';

let contador = ref(1);
let resetCheckFemale = ref();
let resetCheckMale = ref();
let radioButton = ref();
let stopEnter = ref(false);
let warning = ref(false);
let lastName = ref();
let enter = ref();
const listPerson = ref([]);
const bar = ref(null);


const props = defineProps({
    maxNumber: {
        type: Number,
        default: 4,
    },
})

const emits = defineEmits(['aceptSee', 'createList']);

const checkName = (entry, radio) => {

    if (listPerson.value.length == 0) {
        listPerson.value.push([entry, radio]);
        contador.value++;
    } else {
        if (listPerson.value.findIndex((el) => el[0] == entry) == -1 && contador.value != props.maxNumber) {
            listPerson.value.push([entry, radio]);
            warning.value = false;
            contador.value++;
        } else if (listPerson.value.findIndex((el) => el[0] == entry) == -1 && contador.value == props.maxNumber) {
            listPerson.value.push([entry, radio]);
            emits("createList", listPerson.value);
            emits("aceptSee", true);
            stopEnter.value = true;
            warning.value = false;
        } else {
            lastName.value = enter.value;
            warning.value = true;
        }

    }

    resetCheckFemale.value = false;
    resetCheckMale.value = false;
    enter.value = "";
    radioButton.value = "";
}

watch(radioButton, (nv, av) => {

    if (nv == "female") {
        resetCheckFemale.value = true;
        bar.value.focus();
    } else if (nv == "male") {
        resetCheckMale.value = true;
        bar.value.focus();
    }
})


</script>
