<!--
   3. CSS: transform: translate(-50%, -50%); - hvad betyder det??
-->

<script setup>
import { ref } from 'vue';

const menuIsOpen = ref(false); //set to false upon initialization
const openOrClose = ref('open'); //the text that is rendered = when the menu closed, it will say "open"
const buttons = ref(10); // !!! change the number of buttons
const radius = ref(100); //the distance from the mouse position to the buttons
const x = ref(0); //no value yet
const y = ref(0); //no value yet

function canvasHasBeenClicked(event) { //when the canvas has been clicked
  recordMousePosition(event); //executes the function

  if (menuIsOpen.value === false) { //if the menu is closed
    menuIsOpen.value = true; //the menu opens (see v-show)
    openOrClose.value = 'close'; //the text is changed to "close"
  } else {
    menuIsOpen.value = false; //if you click the canvas when the menu is open, the menu closes (see v-show)
    openOrClose.value = 'open'; //text changes to "open"
  }
}

function recordMousePosition(event) {
  x.value = event.pageX; //assigns the mouse-x position (event.pageX) as the value to the x variable
  y.value = event.pageY; //does the same for y
}

function alertTheUser(number) { //when each button is clicked, this function is executed
  alert("You've clicked button number " + number); //it opens a pop-up stating which button has been clicked (the number of the button) 
  //canvasHasBeenClicked(event); //keeps the menu open. it changes the center of the menu to the position of the button, so it is disabled
}
</script>

<template>
  <!-- when the canvas (id of div) is clicked, the function is executed (event listener) -->
  <div id="canvas" @click="canvasHasBeenClicked"> 
    <!-- changes the word in the text to "open" or "close" depending on is the menu is closed or open -->
    <h1 id="clickText">Click anywhere to {{ openOrClose }} the menu!</h1>
    <!-- for-each: for each button in the button "array" (until number of buttons(see variable "buttons")). index number of each button is called "button" -->
    <!-- show if menuIsOpen === true -->
    <!-- if the buttons are clicked, execute funtion alertTheUser using the index-number of the button as an argument in the function -->
    <!-- :style binds the inline style attribute to the button (special syntax for vue): https://vuejs.org/guide/essentials/class-and-style -->
    <!-- left uses cos as it (in the unit circle) represents the x-coordinate of a point along the circumference. top: uses sin as it represents y -->
    <!-- ${x + radius + ...} gives the value of the x-position of the mouse + the radius + ... -->
    <!-- (2 * Math.PI * button) / buttons) is 2π (circumference of unit circle times the button number (position along the circle) / buttons to divide the circle into x number of positions -->
    <!-- `` is used in order to output both the value and px (both a value and and string in one = the whole thing as a string)-->
    <!-- {{ button }} writes number of button on the button --> 
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
    <!-- for only 4 buttons: -->
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

/* top and left places  top-left corner of  element in center, not the actual center of the element.
translate(-50%, -50%) moves the element left and up by half of its width and height putting its center in the center of the canvas. */

button {
  border-radius: 50%;
  padding: 0;
  height: 40px;
  width: 40px;
  border: 1px solid white;
  background-color: DarkOrange;
  color: white;
  transform: translate(-50%, -50%);
}
</style>