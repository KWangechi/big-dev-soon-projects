<template>
  <q-page class="text-center">
    <h5 class="q-mt-sm">Quasar Calculator App</h5>
    <q-card class="card">
      <div class="navbar">
        <span class="calc-text q-ml-sm text-bold">Calc</span>
        <div class="tools">
          <q-toggle
            v-model="lightMode"
            size="2.5rem"
            :icon="!lightMode ? 'light_mode' : 'dark_mode'"
            @click="$q.dark.toggle()"
            color="black"
          ></q-toggle>
        </div>
      </div>
      <div class="screen-2" v-if="previousInput != ''">
        <input type="text" placeholder="0" v-model="previousInput" />
      </div>
      <div class="screen">
        <input type="text" placeholder="0" v-model="currentValue" />
      </div>
      <q-separator></q-separator>
      <div class="calculator-container">
        <div class="row">
          <q-btn class="text-blue-4" rounded @click="clearInput">AC</q-btn>
          <q-btn class="text-blue-4" style="color: aqua" @click="clearPreviousInput"
            >C</q-btn
          >
          <q-btn class="text-blue-4" style="color: aqua" @click="(e) => setSign(e)"
            >%</q-btn
          >
          <q-btn class="text-red-4" @click="(e) => setSign(e)">/</q-btn>
        </div>
        <div class="row">
          <q-btn type="button" @click="(e) => clickNumber(e)">7</q-btn>
          <q-btn type="button" @click="(e) => clickNumber(e)">8</q-btn>
          <q-btn type="button" @click="(e) => clickNumber(e)">9</q-btn>
          <q-btn type="button" class="text-red-4" @click="(e) => setSign(e)">*</q-btn>
        </div>
        <div class="row">
          <q-btn type="button" @click="(e) => clickNumber(e)">4</q-btn>
          <q-btn type="button" @click="(e) => clickNumber(e)">5</q-btn>
          <q-btn type="button" @click="(e) => clickNumber(e)">6</q-btn>
          <q-btn type="button" class="text-red-4" @click="(e) => setSign(e)">-</q-btn>
        </div>
        <div class="row">
          <q-btn type="button" @click="(e) => clickNumber(e)">1</q-btn>
          <q-btn type="button" @click="(e) => clickNumber(e)">2</q-btn>
          <q-btn type="button" @click="(e) => clickNumber(e)">3</q-btn>
          <q-btn type="button" class="text-red-4" @click="(e) => setSign(e)">+</q-btn>
        </div>
        <div class="row q-mb-md">
          <q-btn type="button" class="zero">0</q-btn>
          <q-btn type="button">.</q-btn>
          <q-btn type="button" class="text-center bg-red-3 align-center" @click="getSum"
            >=</q-btn
          >
        </div>
      </div>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, watchEffect } from "vue";

const lightMode = ref(false);
const oldValue = ref(null);
const newValue = ref(null);
const currentValue = ref(null);

let sum = ref(0);
let signSelected = ref("");
const previousInput = ref("");
// const numArray = ref([]);

/**
 * Generic function to get the number clicked(applicable to the number functions)
 */
function clickNumber(e) {
  console.log(currentValue.value);
  currentValue.value =
    currentValue.value == null
      ? e.target.innerText
      : currentValue.value.toString() + e.target.innerText.toString();

  console.log("Current Value: " + currentValue.value);
  // numArray.value.push(e.target.innerText);

  // console.log(numArray.value);

  // should be like a watch thing which tracks what you've clicked
  // newValue.value = e.target.innerText;

  // oldValue.value = newValue.value;

  // console.log(oldValue.value);

  // put the numbers in an array

  // newValue.value =
  //   newValue.value !== null
  //     ? newValue.value?.toString() + e.target.innerText?.toString()
  //     : e.target.innerText?.toString();

  // console.log(parseInt(newValue.value));
}

function setSign(e) {
  signSelected.value = e.target.innerText;

  previousInput.value = oldValue.value + signSelected.value || newValue.value;

  newValue.value = oldValue.value;
  console.log(e.target.innerText);
}

function calculateFunctions() {}

function getSum() {
  console.log(oldValue.value);

  oldValue.value += newValue.value;

  console.log(oldValue.value);
}

function clearInput() {
  sum.value = 0;
  oldValue.value = 0;
  previousInput.value = 0;
  currentValue.value = 0;

  console.log(currentValue.value);
}

function clearPreviousInput() {
  currentValue.value = currentValue.value.slice(0, currentValue.value.length - 1);

  console.log(currentValue.value);
}
</script>

<style scoped>
/* main {
  background-color: black;
} */
.card {
  display: block;
  width: 25%;
  border-radius: 15px;
  background-color: white;
  margin: auto;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.calc-text {
  margin-left: 1rem; /* Adjust margin as needed */
}

.icon {
  margin-left: 10px;
}

.screen {
  display: flex;
  flex-direction: row;
  margin-right: 20px;
  justify-content: end;
  margin-top: 20px;
}

input {
  border: none;
  font-size: 30px;
  max-width: 100%;
  text-align: right;
}

.screen-2 {
  margin-top: 20px;
  margin-right: 15px;
  display: flex;
  justify-content: flex-end;
}

.screen-2 input {
  color: grey;
  text-align: right;

  font-size: 25px;
}

.calculator-container {
  display: grid;
  background-color: white;
  border-radius: 10px;
  margin-bottom: 10px;
}

button {
  width: 60px;
  height: 10px;
  background-color: white;
  border-radius: 5px;
  font-size: 20px;
}

.zero {
  width: 45%;
}

.row {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  padding: 0 10px;
}

@media screen and (min-width: 100px) and (max-width: 850px) {
  .card {
    width: 80%;
  }
}
</style>
