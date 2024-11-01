<script setup>
const props = defineProps(["chats"])

</script>

<template>

    <div class="chatbox">
        <div :class="{ 'user1_chat': mensaje.user === 'left', 'user2_chat': mensaje.user === 'right' }
            "v-for="(mensaje, i) in chats" :key="i" >


            <span class="user_name">{{ mensaje.name }}</span>
            <div class="py-3">
                <p :style="{ backgroundColor: mensaje.color }">{{ mensaje.text }}</p>
            </div>
        </div>
    </div>

</template>

<style scoped>
.chatbox {
    background-color: #303030;
    width: 100%;
    height: 500px;
    overflow: auto;
    background-size: cover;
    padding: 20px;
    border-radius:  10px;
    box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
    border: 1px solid goldenrod;
}

.user1_chat {
    text-align: left;
}

.user2_chat {
    text-align: right;
}

.user1_chat p {
    width: 100%;
    display: inline;
    padding: 10px 20px;
    border-radius: 10px 50px 50px 50px;
    color: #fff;
}
.user2_chat p {
    width: 100%;
    display: inline;
    padding: 10px 20px;
    border-radius: 50px 10px 50px 50px;
    color: #fff;
}


.user_name {
    color: #fff;
}
</style>