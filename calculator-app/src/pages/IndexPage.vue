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
            ><q-icon name="backspace" size="1.5rem"></q-icon
          ></q-btn>
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
          <q-btn type="button" @click="(e) => clickNumber(e)" class="zero">0</q-btn>
          <q-btn type="button">.</q-btn>
          <q-btn
            type="button"
            class="text-center bg-red-3 align-center"
            @click="calculateFunctions"
            >=</q-btn
          >
        </div>
      </div>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from "vue";

const lightMode = ref(false);
const oldValue = ref(null);
const currentValue = ref(null);

let sum = ref(0);
let signSelected = ref("");
const previousInput = ref("");

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
}

/**
 * Set the airthmetic symbol i.e +,-,/,* and %
 */
function setSign(e) {
  console.log(typeof currentValue.value);

  // when a sign is selected, set the currentValue to 0 and then get the currentValue
  signSelected.value = e.target.innerText;

  if (signSelected.value == "%") {
    // get percentage of the number
    currentValue.value = (parseFloat(currentValue.value) / 100).toString();

    return;
  }

  // console.log("When percentage is clicked: " + currentValue.value);

  oldValue.value = parseInt(currentValue.value) || parseFloat(currentValue.value);
  // console.log(oldValue.value);

  previousInput.value =
    oldValue.value.toString() + " " + signSelected.value || currentValue.value;

  currentValue.value = null;
}

function calculateFunctions() {
  previousInput.value = previousInput.value + " " + currentValue.value;
  switch (signSelected.value) {
    case "+":
      getSum();
      break;
    case "-":
      getDifference();
      break;
    case "*":
      getProduct();
      break;
    case "/":
      getQuotient();
      break;
    default:
      break;
  }

  console.log(currentValue.value);
}

/**
 * Calculate sum
 */

function getSum() {
  oldValue.value += parseInt(currentValue.value);
  sum.value = oldValue.value;

  currentValue.value = sum.value;

  console.log(sum.value);
}

/**
 * Calculate the difference
 */

function getDifference() {
  oldValue.value -= parseInt(currentValue.value);
  sum.value = oldValue.value;

  currentValue.value = sum.value;

  console.log(sum.value);
}

/**
 * Calculate Product
 */

function getProduct() {
  oldValue.value *= parseInt(currentValue.value);
  sum.value = oldValue.value;

  currentValue.value = sum.value;

  console.log(sum.value);
}

/**
 * Calculate the division
 */
function getQuotient() {
  oldValue.value /= parseInt(currentValue.value);
  sum.value = oldValue.value;

  currentValue.value = sum.value;

  console.log(sum.value);
}

// /**
//  * Calculate the percentage
//  */
// function getPercentage() {}

function clearInput() {
  sum.value = 0;
  oldValue.value = 0;
  previousInput.value = 0;
  currentValue.value = null;

  console.log(currentValue.value);
}

function clearPreviousInput() {
  currentValue.value =
    typeof currentValue.value == "string"
      ? currentValue.value.slice(0, currentValue.value.length - 1)
      : null;

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
  margin-top: 10px;
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
