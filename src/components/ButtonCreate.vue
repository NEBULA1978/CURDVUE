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
        <textarea v-model="textAreaValue" placeholder="Introduce tu texto aquí"></textarea>
        <button @click="saveTextArea">Guardar texto</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const numButtons = ref(0);
const isBoxExpanded = ref(false);
const textAreaValue = ref('');

const toggleBox = () => {
    isBoxExpanded.value = !isBoxExpanded.value;
};

const createButtons = () => {
    const buttonContainer = document.getElementById('buttonContainer');
    buttonContainer.innerHTML = '';

    for (let i = 1; i <= numButtons.value; i++) {
        const button = document.createElement('button');
        button.innerText = `Botón ${i}`;
        button.addEventListener('click', toggleBox);
        buttonContainer.appendChild(button);
    }
};

const saveTextArea = () => {
    // Do something with the textAreaValue, e.g., send it to the server or process it
    console.log('Texto guardado:', textAreaValue.value);
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
