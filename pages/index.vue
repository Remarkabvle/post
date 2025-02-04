<template>
    <div>
      <div class="container">
        <form action="" @submit.prevent="sendData">
          <input type="text" v-model="name" required />
          <input type="text" v-model="city" required />
          <input type="text" v-model="telefon" required />
          <input type="text" v-model="province" required />
  
          <button type="submit">Send</button>
        </form>
        <p v-if="message">
          {{ message }}
        </p>
      </div>
    </div>
  </template>
  
  <script setup>
  import axios from "axios";
  import { ref, onMounted } from "vue";
  import { useRoute } from "vue-router";
  
  const route = useRoute();
  const name = ref("");
  const city = ref("");
  const telefon = ref("");
  const message = ref("");
  const telegram_id = ref("");
  const province = ref("");
  
  onMounted(() => {
    if (route.query.user_id) {
      telegram_id.value = Number(route.query.user_id);
    }
  });
  
  const sendData = async () => {
    try {
      const response = await axios.post("http://141.145.208.188:8090/update_user", {
        name: name.value,
        shahar: city.value,
        telefon: telefon.value,
        telegram_id: telegram_id.value,
        viloyat: province.value,
      });
  
      message.value = "Malumot yuborildi";
      console.log(response.data);
    } catch (error) {
      message.value = "Xatolik";
      console.error(error);
    }
  };
  </script>
  
  <style>
  .container {
    max-width: 400px;
    margin: 50px auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  form {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  
  input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }
  
  button {
    padding: 10px;
    background-color: #333;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    transition: background 0.3s ease;
  }
  
  button:hover {
    background-color: #555;
  }
  
  p {
    margin-top: 10px;
    font-size: 14px;
    color: green;
  }
  </style>
  