<template>
    <div class="flex justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96">
            <div class="flex flex-col text-xl text-blue-700 items-center">
                <label for="name">Introduzca persona {{ contador }}</label>
                <input v-model="enter" @keyup.enter="enterPerson" type="text" name="name"
                    class="rounded border mb-2 border-blue-700 w-36 text-center">
                <input type="radio" id="uno" value="female" name="gender" :checked="resetCheck" v-model="radioButton">
                <label for="uno">Mujer</label>
                <input type="radio" id="Dos" value="male" name="gender" :checked="resetCheck" v-model="radioButton">
                <label for="Dos">Hombre</label>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

let contador = ref(1);
let resetCheck = ref();
let radioButton = ref();

const props = defineProps({
    maxNumber: {
        type: Number,
        default:2,
    }
})

let enter = ref();

const emits = defineEmits(['enterPerson', 'aceptSee','createList'])

const enterPerson = () => {
    
    emits("enterPerson", enter.value,radioButton.value);

    if(contador.value != props.maxNumber){
        contador.value++;
    }else{
        emits("createList") ;
        emits("aceptSee", true);
        
    }  
    console.log(contador.value)
    console.log(props.maxNumber)
    enter.value = "";
}

</script>
