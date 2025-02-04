<script setup>
import { useRoute } from "vue-router";
import { ref } from "vue";

const route = useRoute();
const userId = ref(null);

if (route.query.user_id) {
  userId.value = Number(route.query.user_id);
}

console.log("User ID:", userId.value);
</script>

<template>
  <p>User ID: {{ userId }}</p>
</template>
