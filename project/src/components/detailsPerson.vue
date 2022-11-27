<template>
    <div class="flex p-10 justify-center rounded border-2 border-amber-700 gap-5">
        
        <div class="flex flex-col pt-5 items-center w-56 h-56 rounded border-2 border-blue-900">
            <div>
                <h1>Nombre: {{ rName1 }}</h1>
            </div>
            <div class="mb-5 mt-5 mx-2">
                <img class="rounded-full" :src=rPhoto1 alt="foto perfil">
            </div>
        </div>

        <div class="flex flex-col pt-5 items-center w-56 h-56 rounded border-2 border-blue-900">
            <div>
                <h1>Nombre: {{ rName2 }}</h1>
            </div>
            <div class="mb-5 mt-5 mx-2">
                <img class="rounded-full" :src=rPhoto2 alt="foto perfil">
            </div>
        </div>
    </div>

</template>

<script setup>

import { ref } from 'vue';


let rName1 = ref(props.name1);
let rPhoto1 = ref(props.photo1);
let rName2 = ref(props.name2);
let rPhoto2 = ref(props.photo2);



const props = defineProps({
    name1: {
        type: String,


    }, photo1: {
        type: String,

    },
    name2: {
        type: String,


    }, photo2: {
        type: String,

    }
})

</script>


