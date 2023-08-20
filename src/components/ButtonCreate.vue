<template>
    <div>
        <input v-model="numButtons" type="number" placeholder="Número de botones" />
        <button @click="createButtons">Crear botones</button>
        <div id="buttonContainer">
            <button v-for="buttonIndex in numButtons" :key="buttonIndex" @click="toggleBox">
                Botón {{ buttonIndex }}
            </button>
        </div>
        <div :class="{ test: isBoxExpanded }" id="testbox"></div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const numButtons = ref(0);
const isBoxExpanded = ref(false);

const toggleBox = () => {
    isBoxExpanded.value = !isBoxExpanded.value;
};

const createButtons = () => {
    const buttonContainer = document.getElementById('buttonContainer');
    buttonContainer.innerHTML = '';

    for (let i = 1; i <= numButtons.value; i++) {  // Start button index from 1
        const button = document.createElement('button');
        button.innerText = `Botón ${i}`;  // Set button text
        button.addEventListener('click', toggleBox);
        buttonContainer.appendChild(button);
    }
};
</script>

<style>
#testbox {
    opacity: 0;
    width: 300px;
    height: 0px;
    background-color: blue;
}

#testbox.test {
    opacity: 1;
    height: 300px;
    transition: opacity 1s ease-in-out, height 0.5s ease-in-out;
}
</style>
