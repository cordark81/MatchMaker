<template>
    <div class="flex justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96">
            <div class="flex flex-col text-xl text-blue-700 items-center">
                <label for="name">¿Cuantas personas van a hacer Match?</label>
                <countPerson @numberPerson=goUp />
            </div>
        </div>
    </div>
</template>

<script setup>

import countPerson from './countPerson.vue';


const emits = defineEmits(['numberPerson'])

const goUp = (emit) => {
    
    emits("numberPerson",emit);
}





</script>
