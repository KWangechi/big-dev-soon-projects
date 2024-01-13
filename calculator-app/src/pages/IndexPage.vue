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
  width: 400px;
  height: 350px;
  border-radius: 10px;
  background-color: white;
  margin: auto;
  display: grid;
}

.navbar {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  margin-top: 20px;
  height: max-content;
}

.tools {
  margin: 0 15px;
  height: max-content;
}
.icon {
  margin-left: 10px;
}

.screen {
  display: flex;
  margin-top: -150px;
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
</style>
