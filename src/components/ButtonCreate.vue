<template>
    <div>
        <input v-model="numButtons" type="number" placeholder="Número de botones" />
        <button @click="createButtons">Crear botones</button>
        <div id="buttonContainer">
            <button v-for="buttonIndex in numButtons" :key="buttonIndex" @click="toggleBox(buttonIndex)">
                Botón {{ buttonIndex }}
            </button>
        </div>
        <div :class="{ test: isBoxExpanded }" id="testbox">
            <div v-for="(savedText, index) in savedTexts" :key="index">{{ savedText }}</div>
        </div>
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
const savedTexts = ref([]);

const toggleBox = (buttonIndex) => {
    isBoxExpanded.value = !isBoxExpanded.value;
    console.log(`Botón ${buttonIndex} clicado`);
};

const createButtons = () => {
    buttonTexts.value = Array.from({ length: numButtons.value }, (_, index) => `Botón ${index + 1}`);
};

const saveTextArea = () => {
    savedTexts.value.push(textAreaValue.value);
    textAreaValue.value = '';
};
</script>

<style>
#testbox {
    opacity: 0;
    width: 300px;
    background-color: blue;
    padding: 10px;
}

#testbox.test {
    opacity: 1;
    transition: opacity 1s ease-in-out;
}
</style>
