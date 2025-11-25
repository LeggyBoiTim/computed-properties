<script setup>
import { ref, computed } from 'vue';

const people = ref([
    { name: 'Jan', age: 12 }, 
    { name: 'Piet', age: 20 }, 
    { name: 'Herman', age: 65 }, 
    { name: 'Ivan', age: 5 }, 
    { name: 'Tom', age: 43 }
]);

const newName = ref(null);
const newAge = ref(null);

const children = computed(() => {
    return people.value.filter((person) => person.age < 18);
});

const adults = computed(() => {
    return people.value.filter((person) => person.age >= 18);
});

const totalPeople = computed(() => {
    return people.value.length;
});

const numberOfChildren = computed(() => {
    return children.value.length;
});

const addPerson = () => {
    if (newName.value && newAge.value) {
        people.value.push({name: newName.value, age: newAge.value});
        newName.value = null;
        newAge.value = null;
    }
};
</script>



<template>
    <input v-model="newName" placeholder="Naam" type="text">
    <input v-model.number="newAge" placeholder="Leeftijd" type="number">

    <button @click="addPerson">Toevoegen</button>

    <ul>
        <li v-for="(person, index) in people" :key="index">
            {{ person.name }}, {{ person.age }} jaar oud
        </li>
    </ul>

    <p>Kinderen:</p>
    <ul>
        <li v-for="(person, index) in children" :key="index">
            {{ person.name }}, {{ person.age }} jaar oud
        </li>
    </ul>

    <p>Volwassenen:</p>
    <ul>
        <li v-for="(person, index) in adults" :key="index">
            {{ person.name }}, {{ person.age }} jaar oud
        </li>
    </ul>

    <p>Aantal personen: {{ totalPeople }}</p>
    <p>Aantal kinderen: {{ numberOfChildren }}</p>
</template>



<style scoped>
</style>
