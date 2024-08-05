<script setup>
import { ref } from "vue";
const qrImage = ref("");
const qrLink = ref("");
const showImg = ref(false);
const error = ref(false);

function generateQrCode() {
  if (qrLink.value.length > 0 && qrLink.value.includes("https://")) {
    qrImage.value = `https://api.qrserver.com/v1/create-qr-code/?size=300x300&data=${qrLink.value}`;
    showImg.value = true;
  } else {
        error.value = true;
        qrLink.value = "Enter a valid link";
        setTimeout(() => {
            error.value = false;
            qrLink.value = "";
        }, 800);
    } 

}
</script>

<template>
  <div class="container">
    <p>Enter your URL</p>
    <input type="text" placeholder="URL" v-model="qrLink" :class="{ 'error': error }"/>
    <div :class="{ 'show-img': showImg }" id="imgBox">
    <img :src="qrImage" id="qrImage">
  </div>
    <button @click="generateQrCode">Generate QR Code</button>
  </div>
</template>

<style scoped>
.container {
  width: 400px;
  padding: 25px 35px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #d9d9d9;
  border-radius: 10px;
  color: #0d0d0d;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
}

.container p {
  font-weight: 600;
  font-size: 16px;
  margin-bottom: 8px;
}

.container input {
  width: 100%;
  height: 50px;
  border: 1px solid #d9c1b4;
  outline: 0;
  padding: 10px;
  margin: 10px 0 20px;
  border-radius: 5px;
}

.container button {
  width: 100%;
  height: 50px;
  background: #8c7b74;
  color: #fff;
  border: 0;
  outline: 0;
  border-radius: 5px;
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  margin: 20px 0;
  font-weight: 500;
  transition: background 0.5s;
}

.container button:hover{
    background: #6b5f5a;
}

#imgBox {
  width: 300px;
  border-radius: 5px;
  max-height: 0;
  overflow: hidden;
  transform: max-height 1s;
}

#imgBox img {
  width: 100%;
  padding: 10px;
  transition: 0.5s;
}

#imgBox img:hover{
  transform: scale(1.05);
}

#imgBox.show-img {
    max-height: 300px;
    margin: 10px auto;
    border: 1px solid #d1d1d1;
}

.error {
    border: 1px solid red !important;
    animation: shake 0.1s linear 10;
    color: red;
}

@keyframes shake {
    0%{
        transform: translateX(0);
    }
    25%{
        transform: translateX(-4px);
    }
    50%{
        transform: translateX(0);
    }
    75%{
        transform: translateX(4px);
    }
    100%{
        transform: translateX(0);
    }
}
</style>
