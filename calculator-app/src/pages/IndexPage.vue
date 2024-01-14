<template>
  <q-page class="container text-center">
    <h5 class="q-mt-xl">Quasar Calculator App</h5>
    <div class="card">
      <div class="navbar">
        <p class="calc-text q-mx-lg">Calc</p>
        <div class="tools">
          <q-icon name="dark_mode" size="1.3rem" class="icon"></q-icon>
          <q-icon name="light_mode" size="1.3rem" class="icon"></q-icon>
        </div>
      </div>
      <div class="screen">
        <input type="text" placeholder="0" />
      </div>
      <div class="calculator-container">
        <div class="row">
          <button type="button">AC</button>
          <button type="button">C</button>
          <button type="button">%</button>
          <button type="button">/</button>
        </div>
        <div class="row">
          <button type="button">7</button>
          <button type="button">8</button>
          <button type="button">9</button>
          <button type="button">X</button>
        </div>
        <div class="row">
          <button type="button">4</button>
          <button type="button">5</button>
          <button type="button">6</button>
          <button type="button">-</button>
        </div>
        <div class="row">
          <button type="button">1</button>
          <button type="button">2</button>
          <button type="button">3</button>
          <button type="button">+</button>
        </div>
        <div class="row">
          <button type="button" class="zero">0</button>
          <button type="button">.</button>
          <button type="button">=</button>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
});
</script>

<style scoped>
.card {
  display: block;
  width: 300px;
  height: 350px;
  border-radius: 15px;
  background-color: white;
  margin: auto;
}

.navbar {
  display: flex;
  justify-content: space-between;
  padding-top: 20px;
  height: max-content;
}

.tools {
  margin: 0 15px;
  height: max-content;
  margin-top: 30p;
}
.icon {
  margin-left: 10px;
}

.screen {
  display: flex;
  margin-right: 20px;
  align-items: flex-start;
  justify-content: space-between;
  height: max-content;
  direction: rtl;
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
  min-height: 246px;
  margin-top: 10px;
}
button {
  width: 45px;
  height: 30px;
  background-color: white;
  border-radius: 5px;
}

.zero {
  width: 120px;
}

.row {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
  padding: 0 10px;
}
</style>
