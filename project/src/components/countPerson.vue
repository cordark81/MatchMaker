<template>
    <div class="flex flex-row my-5 ">
        <button @click="countLess" class="mr-5 bg-gray-300 w-8 h-8 rounded">-</button>
        <h1>{{ count }}</h1>
        <button @click="countPlus" class="ml-5 bg-gray-300 w-8 h-8 rounded">+</button>
    </div>
</template>

<script setup>
import { ref, watch} from 'vue';

const count = ref(4);

const countPlus  = ()=>{
    count.value != 20 ? count.value += 2:count.value=count.value;
};

const countLess  = ()=>{
    count.value != 4 ? count.value -= 2:count.value=count.value;
};

const emits = defineEmits(['numberPerson'])

watch(count,(nv,av)=>{
    
    emits("numberPerson",nv);
    
});


</script>

<style lang="scss" scoped>

</style>