<template>
  <q-layout class="bg-blue-4">
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "MainLayout",

  setup() {
    // const leftDrawerOpen = ref(false)

    return {};
  },
});
</script>
