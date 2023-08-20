<template>
    <div>
        <input v-model="numButtons" type="number" placeholder="Número de botones" />
        <button @click="createButtons">Crear botones</button>
        <div id="buttonContainer">
            <button v-for="(button, buttonIndex) in buttonTexts" :key="buttonIndex" @click="toggleBox(buttonIndex)">
                {{ button.text }}
            </button>
        </div>
        <div :class="{ test: isBoxExpanded !== -1 }" id="testbox">
            <div v-for="(button, index) in buttonTexts" :key="index">
                <div v-if="index === isBoxExpanded">
                    <div v-for="(savedText, textIndex) in button.savedTexts" :key="textIndex">{{ savedText }}</div>
                </div>
            </div>
        </div>
        <textarea v-model="textAreaValue" placeholder="Introduce tu texto aquí"></textarea>
        <button @click="saveTextArea">Guardar texto</button>
        <input type="file" @change="loadFile" accept=".sh,.py,.js" />
    </div>
</template>

<script setup>
import { ref } from 'vue';

const numButtons = ref(0);
const isBoxExpanded = ref(-1);
const textAreaValue = ref('');
const buttonTexts = ref([]);

const toggleBox = (buttonIndex) => {
    isBoxExpanded.value = isBoxExpanded.value === buttonIndex ? -1 : buttonIndex;
    console.log(`Botón ${buttonIndex + 1} clicado`);
};

const createButtons = () => {
    buttonTexts.value = Array.from({ length: numButtons.value }, (_, index) => ({
        text: `Botón ${index + 1}`,
        savedTexts: [],
    }));
};

const saveTextArea = () => {
    if (isBoxExpanded.value !== -1) {
        buttonTexts.value[isBoxExpanded.value].savedTexts.push(textAreaValue.value);
        textAreaValue.value = '';
    }
};

const loadFile = (event) => {
    const file = event.target.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
            if (isBoxExpanded.value !== -1) {
                buttonTexts.value[isBoxExpanded.value].savedTexts.push(e.target.result);
            }
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
