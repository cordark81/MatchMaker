<template>
        <div class="flex justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96">
            <div class="flex flex-col text-xl text-blue-700 items-center">
                <label for="name">Introduzca persona {{number}}</label>
                <input v-model="enter" @keyup.enter="enterPerson" type="text" name="name" class="rounded border mb-2 border-blue-700">
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
	number: {
		type: Number,
	},
})

let enter = ref();

const emits = defineEmits(['enterPerson'])

const enterPerson = () => {
    
    emits("enterPerson",enter.value);
}

</script>

<style lang="scss" scoped>

</style>