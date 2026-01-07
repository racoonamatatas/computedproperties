<template>
    <input v-model.trim="newName" type="text" placeholder="Name" />
    <input v-model.number="newAge" placeholder="Age" />
    <button @click="addPerson">Add</button>

    <ul>
        People:
        <br />
        <li v-for="person in people" :key="person.name">{{ person.name }} {{ person.age }}</li>
    </ul>
    <ul>
        Children:
        <li v-for="child in children" :key="child.name">{{ child.name }} {{ child.age }}</li>
    </ul>
</template>

<script setup>
import {ref, computed} from 'vue';

const people = ref([
    {name: 'Jan', age: 12},
    {name: 'Piet', age: 20},
]);

let newName = ref('');
let newAge = ref();

// Adds a new person to the reactive people array.
const addPerson = () => {
    people.value.push({name: newName.value, age: newAge.value});

    // reset the ref values
    newName.value = '';
    newAge.value = null;
};

// Computed array of children in the people array.
const children = computed(() => people.value.filter(person => person.age < 18));
</script>
