<template>
  <router-view />
</template>

<script setup>
import { ref, provide } from "vue";
import { onAuthStateChanged } from "firebase/auth";
import { auth } from "./firebase";

const userGoogle = ref(false);
provide('userGoogle', userGoogle);

onAuthStateChanged(auth, (user) => {
  userGoogle.value = user;
});

</script>
