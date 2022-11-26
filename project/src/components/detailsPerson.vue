<template>

    <div class="flex flex-col pt-5 items-center w-56 h-56 rounded border-2 border-blue-900">
        <div>
            <h1>Nombre: {{ rName }}</h1>
        </div>
        <div class="mb-5 mt-5 mx-2">
            <img class="rounded-full" :src=rPhoto alt="foto perfil">
        </div>
    </div>

</template>

<script setup>

import { ref } from 'vue';


let rName = ref(props.name);
let rPhoto = ref(props.photo);


const props = defineProps({
    name: {
        type: String,


    }, photo: {
        type: String,

    }
})

</script>


