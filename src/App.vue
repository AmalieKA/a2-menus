<!--
  1. :style
  2. find lige ud af hvordan sin/cos bliver regnet ud til at blive x og y + regnestykket med 2pi
  3. CSS: transform: translate(-50%, -50%); - hvad betyder det??
-->

<script setup>
import { ref } from 'vue';

const menuIsOpen = ref(false);
const openOrClose = ref('open');
const buttons = ref(10); // !!! change the number of buttons
const radius = ref(100);
const x = ref(0);
const y = ref(0);

function canvasHasBeenClicked(event) {
  recordMousePosition(event);

  if (menuIsOpen.value === false) {
    menuIsOpen.value = true;
    openOrClose.value = 'close';
  } else {
    menuIsOpen.value = false;
    openOrClose.value = 'open';
  }
}

function recordMousePosition(event) {
  x.value = event.pageX;
  y.value = event.pageY;
}

function alertTheUser(number) {
  alert("You've clicked button number " + number);
  canvasHasBeenClicked(event);
}
</script>

<template>
  <div id="canvas" @click="canvasHasBeenClicked">
    <h1 id="clickText">Click anywhere to {{ openOrClose }} the menu!</h1>
    <button
      v-for="button in buttons"
      v-show="menuIsOpen"
      @click="alertTheUser(button)"
      :style="{
        position: 'absolute',
        left: `${x + radius * Math.cos((2 * Math.PI * button) / buttons)}px`,
        top: `${y + radius * Math.sin((2 * Math.PI * button) / buttons)}px`,
      }"
    >
      {{ button }}
    </button>
    <!-- <button
      id="button1"
      v-show="menuIsOpen"
      @click="alertTheUser(1)"
      :style="{
        position: 'absolute',
        left: `${x}px`,
        top: `${y - radius}px`,
      }"
    >
      1
    </button>
    <button
      id="button2"
      v-show="menuIsOpen"
      @click="alertTheUser(2)"
      :style="{
        position: 'absolute',
        left: `${x + radius}px`,
        top: `${y}px`,
      }"
    >
      2
    </button>
    <button
      id="button3"
      v-show="menuIsOpen"
      @click="alertTheUser(3)"
      :style="{
        position: 'absolute',
        left: `${x}px`,
        top: `${y + radius}px`,
      }"
    >
      3
    </button>
    <button
      id="button4"
      v-show="menuIsOpen"
      @click="alertTheUser(4)"
      :style="{
        position: 'absolute',
        left: `${x - radius}px`,
        top: `${y}px`,
      }"
    >
      4
    </button> -->
  </div>
</template>

<style>
#canvas {
  min-width: 100%;
  min-height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgb(180, 150, 180);
  font-family: Verdana, sans-serif;
  text-align: center;
}

#clickText {
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

button {
  border-radius: 50%;
  padding: 0;
  height: 40px;
  width: 40px;
  border: 1px solid white;
  background-color: DarkOrange;
  color: white;
}
</style>