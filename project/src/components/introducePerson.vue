<template>
    <div class="flex justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96">
            <div class="flex flex-col text-xl text-blue-700 items-center">
                <label for="name">Introduzca persona {{ contador }}</label>
                <input ref="bar" v-model="enter" @keyup.enter="enterPerson" type="text" name="name"
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
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';

let contador = ref(1);
let resetCheckFemale = ref();
let resetCheckMale = ref();
let radioButton = ref();
let stopEnter = ref(false);
const bar = ref(null);

const props = defineProps({
    maxNumber: {
        type: Number,
        default: 4,
    }
})

let enter = ref();

const emits = defineEmits(['enterPerson', 'aceptSee', 'createList'])

const enterPerson = () => {

    emits("enterPerson", enter.value, radioButton.value);

    if (contador.value != props.maxNumber) {
        contador.value++;
    } else {
        emits("createList");
        emits("aceptSee", true);
        stopEnter.value = true;

    }
    
    resetCheckFemale.value = false;
    resetCheckMale.value = false;
    enter.value = "";
    
}

watch(radioButton, (nv, av) => {

    if (nv == "female") {
        resetCheckFemale.value = true;
        bar.value.focus();
    } else if (nv == "male") {
        resetCheckMale.value = true;
        bar.value.focus();
    }
});


// no funciona para el reset del check const voidCheck = computed(() => resetCheck.value==true?resetCheck.value=false:resetCheck.value=true);

</script>
