<template>
    <div class="flex justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96">
            <div class="flex flex-col text-xl text-blue-700 items-center">
                <label for="name">Introduzca persona {{ contador }}</label>
                <input ref="bar" v-model="enter" @keyup.enter="enterPerson" type="text" name="name"
                    class="rounded border mb-2 border-blue-700 w-36 text-center" :disabled="stopEnter">
                
                <div class="flex items-baseline">
                    <label for="uno">Mujer</label>
                    <input  class="ml-2" type="radio" id="uno" value="female" name="gender" :checked="resetCheck"
                        v-model="radioButton" :disabled="stopEnter" @click=this.$refs.bar.focus()>
                    <label class="ml-5" for="Dos">Hombre</label>
                    <input class="ml-2" type="radio" id="Dos" value="male" name="gender" :checked="resetCheck" v-model="radioButton"
                        :disabled="stopEnter" @click=this.$refs.bar.focus()>
                </div>

            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

let contador = ref(1);
let resetCheck = ref();
let radioButton = ref();
let stopEnter = ref(false);

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
    
    enter.value = "";
    // funciona solo una vez resetCheck.value = false;

    
}

// no funciona para el reset del check const voidCheck = computed(() => resetCheck.value==true?resetCheck.value=false:resetCheck.value=true);
 
</script>
