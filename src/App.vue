<template>
    <input v-model.trim="newName" type="text" placeholder="Name" />
    <input v-model.number="newAget" placeholder="Age" />
</template>

<script setup>
import {ref} from 'vue';

const people = ref([
    {name: 'Jan', age: 12},
    {name: 'Piet', age: 20},
]);

let newName = ref('');
let newAge = ref();
</script>
