<template>
    <div class="flex justify-center mt-10">
        <div class="border-2 border-red-600 flex flex-col text-center w-96 h-32">
            <div class="flex flex-col pt-5 text-lg text-blue-700 items-center">
                <label for="file" >Pincha para seleccionar fichero</label>
                <input type="file" @change="loadTextFromFile" name="file">
            </div>
        </div>
    </div>
</template>

<script setup>

const emits = defineEmits(['load']);

const loadTextFromFile = (ev) => {
    const file = ev.target.files[0];
    const reader = new FileReader();
    reader.onload = e => emits("load", e.target.result);
    reader.readAsText(file);
}


</script>

