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
      <div class="screen">
        <input type="text" placeholder="0" v-model="calcInput" />
      </div>
      <div class="screen">
        <input type="text" placeholder="0" v-model="calcInput" />
      </div>
      <q-separator></q-separator>
      <div class="calculator-container">
        <div class="row">
          <q-btn class="text-blue-4" rounded>AC</q-btn>
          <q-btn class="text-blue-4" style="color: aqua" @click="clearInput">C</q-btn>
          <q-btn class="text-blue-4" style="color: aqua" @click="(e) => setSign(e)"
            >%</q-btn
          >
          <q-btn class="text-red-4" @click="(e) => setSign(e)">/</q-btn>
        </div>
        <div class="row">
          <q-btn type="button">7</q-btn>
          <q-btn type="button">8</q-btn>
          <q-btn type="button">9</q-btn>
          <q-btn type="button" class="text-red-4" @click="(e) => setSign(e)">X</q-btn>
        </div>
        <div class="row">
          <q-btn type="button">4</q-btn>
          <q-btn type="button">5</q-btn>
          <q-btn type="button">6</q-btn>
          <q-btn type="button" class="text-red-4" @click="(e) => setSign(e)">-</q-btn>
        </div>
        <div class="row">
          <q-btn type="button" @click="clickOne">1</q-btn>
          <q-btn type="button">2</q-btn>
          <q-btn type="button">3</q-btn>
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
const calcInput = ref(null);
let sum = ref(0);
let signSelected = ref("");

function clickOne() {
  calcInput.value = 1;
}

function setSign(e) {
  signSelected.value = e.target.innerText;

  console.log(e.target.innerText);
  // calcInput.value = "-";
}
function getSum() {
  sum.value = calcInput.value;

  // console.log(calcInput.value + calcInput.value);
}

function clearInput() {
  sum.value = 0;
  calcInput.value = 0;
}
watchEffect(() => {
  console.log(calcInput.value);
});
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

/* .navbar {
  display: flex;
  justify-content: space-between;
  padding-top: 20px;
}

.navbar > .tools {
  display: flex;
  justify-content: flex-end;
} */

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
  margin-right: 20px;
  align-items: flex-start;
  justify-content: space-between;
  direction: rtl;
  margin-top: 35px;
}

input {
  border: none;
  font-size: 30px;
  max-width: 100%;
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
} ;
</style>
