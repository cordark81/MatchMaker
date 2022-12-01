<template>
    <div class="flex justify-around mt-40 xl:mt-32">    
        <div>
            <h1 class="text-center mb-5 font-bold text-blue-900">Por archivo</h1>
            <button @click="forFile"><img
                    class=" w-36 h-36 xl:w-52 xl:h-52 rounded-full shadow-xl hover:scale-110 transition duration-500"
                    src="../assets/carpeta-removebg-preview-removebg-preview.jpg" alt="carpeta"></button>
        </div>
        <div>
            <h1 class="text-center mb-5 font-bold text-blue-900">Crear una lista</h1>
            <button @click="createList"><img
                    class=" w-36 h-36 xl:w-52 xl:h-52 rounded-full shadow-xl hover:scale-110 transition duration-500"
                    src="../assets/images-removebg-preview.jpg" alt="carpeta"></button>
        </div>
    </div>
</template>

<script setup>

const emits = defineEmits(['forFile','createList']);

const forFile = () => emits('forFile');
const createList = () => emits('createList');
</script>

<style lang="scss" scoped>

</style>