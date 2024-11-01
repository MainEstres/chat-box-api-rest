<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';
import ChatBox from './components/ChatBox.vue';

const users = ref([])
const users1 = ref(null);
const users2 = ref(null);
console.log(users1.value)



const text1 = ref('');
const text2 = ref('');

const color1 = ref('#525298')
const color2 = ref('#524587');

const chats = ref([]);
console.log(chats.value)

const enviarMensaje = (user) => {
  if (user === 'left' && text1.value.trim()) {
    chats.value.push({ user: 'left', text: text1.value, name: `${users1.value.name.first} ${users1.value.name.last} `, color: color1.value });
    text1.value = "";
  }
  if (user === 'right' && text2.value.trim()) {
    chats.value.push({ user: 'right', text: text2.value, name: `${users2.value.name.first} ${users2.value.name.last}`, color: color2.value });
    text2.value = "";
  }
}

const getUsuarios = async () => {
  try {
    const url = 'https://randomuser.me/api/?results=2'
    const { data } = await axios.get(url);
    users.value = data.results

    users1.value = users.value[0];
    users2.value = users.value[1];



  } catch (error) {
    console.log(error)
  }
}

onMounted(getUsuarios);
</script>

<template>
  
  <section class="container">
    <h1 class="text-center mt-4">ChatBox API REST</h1>
    <div class="row box">
      <div class="col card me-3" style="width: 14rem;">
        <div class="img-fluid text-center " v-if="users1">
          <img class="rounded-circle" :src="users1.picture.large">
          <h5>{{ users1.name.first }} {{ users1.name.last }}</h5>
        </div>
        <input v-model="color1" value="#00000" class="w-100" type="color">
        <textarea v-model="text1"></textarea>
        <button @click="enviarMensaje('left')">Enviar</button>
      </div>

      <div class="col">
        <ChatBox  :chats="chats" />
      </div>

      <div class="col card ms-3" style="width: 14rem;">
        <div v-if="users2" class="img-fluid text-center">
          <img class="rounded-circle" :src="users2.picture.large">
          <h5>{{ users2.name.first }} {{ users2.name.last }}</h5>
        </div>
        <input v-model="color2" value="#fffff" class="w-100" type="color">
        <textarea v-model="text2"></textarea>
        <button @click="enviarMensaje('right')">Enviar</button>
      </div>
    </div>

  </section>

</template>

<style scoped>
.box {
  margin-top: 5rem;
}
</style>