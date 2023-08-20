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
        <input type="file" @change="loadFile" accept=".sh,.py,.js" />
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

const loadFile = (event) => {
    const file = event.target.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
            textAreaValue.value = e.target.result;
        };
        reader.readAsText(file);
    }
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
