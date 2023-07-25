<template>
  <div>
    <button @click="generateSheet">Generate Random Sheet Music</button>
    <div ref="sheetContainer" class="sheet-container"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import abcjs from 'abcjs';

const sheetContainer = ref();

const generateSheet = () => {
  // Clear previous sheet music
  sheetContainer.value.innerHTML = '';

  // Generate random notes (you can customize this part)
  const notes = generateRandomNotes();
  const abcNotation = `X:1\nM:4/4\nK:C\n${notes.join(' ')}`;
  abcjs.renderAbc(sheetContainer.value, abcNotation, {});
};

const generateRandomNotes = () => {
  const availableNotes = ['C', 'D', 'E', 'F', 'G', 'A', 'B'];
  const availableOctaves = ['3', '4', '5'];
  const numNotes = 16; // Number of random notes to generate
  const notes = [];

  for (let i = 0; i < numNotes; i++) {
    const randomNote = availableNotes[Math.floor(Math.random() * availableNotes.length)];
    const randomOctave = availableOctaves[Math.floor(Math.random() * availableOctaves.length)];
    const note = `${randomNote}${randomOctave}`;
    notes.push(note);
  }

  return notes;
};

onMounted(() => {
  generateSheet();
});
</script>

<style>
  .sheet-container {
    display: inline-block;
    border: 1px solid black;
  }
</style>
