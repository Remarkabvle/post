<template>
  <div class="container">
    <form @submit.prevent="sendData">
      <label>
        Ismingiz
        <input type="text" maxlength="50"  v-model="name" placeholder="Ismingizni kiriting" required />
      </label>
      <label>
        Viloyat
        <input type="text" maxlength="30"  v-model="province" placeholder="Viloyatingizni kiriting" required />
      </label>
      <label>
        Shahar
        <input type="text"  maxlength="30" v-model="city" placeholder="Shaharingizni kiriting" required />
      </label>
      <label>
        Telefon
        <input type="text"  maxlength="14" v-model="telefon" placeholder="Telefon raqamingiz" required />
      </label>
      <button type="submit">Yuborish</button>
    </form>
    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from '#app'

const route = useRoute()
const router = useRouter()

const name = ref("")
const city = ref("")
const telefon = ref("")
const message = ref("")
const telegram_id = ref("")
const province = ref("")

onBeforeMount(() => {
  if (route.query.user_id) {
    telegram_id.value = Number(route.query.user_id)
  }
})

const sendData = async () => {
  try {
    await $fetch("http://grscan.uz/update_user", {
      method: 'POST',
      body: {
        name: name.value,
        shahar: city.value,
        telefon: telefon.value,
        telegram_id: telegram_id.value,
        viloyat: province.value,
      }
    })
    message.value = "Ma'lumot yuborildi"
  } catch (error) {
    message.value = "Xatolik yuz berdi"
  }
}
</script>

<style scoped>
.container {
  width: 100%;
  max-width: 100vw;
  margin: 0;
  padding: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-sizing: border-box;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;
}

label {
  font-size: 16px;
  color: #333;
  width: 100%;
  display: flex;
  flex-direction: column;
}

input {
  width: 100%;
  padding: 14px;
  border: 2px solid #aaa;
  border-radius: 8px;
  font-size: 18px;
  background-color: #f9f9f9;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 14px;
  background: #333;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background: #555;
}

p {
  margin-top: 10px;
  font-size: 16px;
  color: green;
  text-align: center;
}
</style>