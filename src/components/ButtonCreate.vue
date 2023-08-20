<template>
    <div>
        <input v-model="numButtons" type="number" placeholder="Número de botones" />
        <button @click="createButtons">Crear botones</button>
        <div id="buttonContainer">
            <button v-for="buttonIndex in numButtons" :key="buttonIndex" @click="toggleBox(buttonIndex)">
                Botón {{ buttonIndex }}
            </button>
        </div>
        <div :class="{ test: isBoxExpanded }" id="testbox">{{ savedText }}</div>
        <textarea v-model="textAreaValue" placeholder="Introduce tu texto aquí"></textarea>
        <button @click="saveTextArea">Guardar texto</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const numButtons = ref(0);
const isBoxExpanded = ref(false);
const textAreaValue = ref('');
const buttonTexts = ref([]);
const savedText = ref('');

const toggleBox = (buttonIndex) => {
    isBoxExpanded.value = !isBoxExpanded.value;
    console.log(`Botón ${buttonIndex} clicado`);
};

const createButtons = () => {
    buttonTexts.value = Array.from({ length: numButtons.value }, (_, index) => `Botón ${index + 1}`);
};

const saveTextArea = () => {
    savedText.value = textAreaValue.value;
    textAreaValue.value = '';
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
