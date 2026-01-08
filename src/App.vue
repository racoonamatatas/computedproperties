<template>
    <input v-model.trim="newName" type="text" placeholder="Name" />
    <input v-model.number="newAge" placeholder="Age" />
    <button @click="addPerson">Add</button>

    <ul>
        People:
        <br />
        <li v-for="(person, index) in people" :key="index">{{ person.name }} {{ person.age }}</li>
    </ul>
    <ul>
        Children:
        <li v-for="(child, index) in children" :key="index">{{ child.name }} {{ child.age }}</li>
    </ul>
    <ul>
        Adults:
        <li v-for="(adult, index) in adults" :key="index">{{ adult.name }} {{ adult.age }}</li>
    </ul>
    <p>Total number of people: {{ totalPeople }}</p>
    <p>Total number of children: {{ numberOfChildren }}</p>
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

const isAdult = person => {
    return person.age >= 18;
};

// Computed array of children in the people array.
const children = computed(() => people.value.filter(person => !isAdult(person)));

// Computed array of adults in the people array.
const adults = computed(() => people.value.filter(isAdult));

const totalPeople = computed(() => people.value.length);

const numberOfChildren = computed(() => children.value.length);
</script>
