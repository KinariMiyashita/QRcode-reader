<script setup>
import { QrcodeStream, QrcodeDropZone, QrcodeCapture } from 'vue-qrcode-reader';
const value = ref();
const isQrcode = ref(false);

// const onDetect = (content) => {
//   value.value = content[0].rawValue;
// };

const handleButton = (content) => {
  isQrcode.value = !isQrcode.value;
};
</script>
<template>
  <div class="app">
    <h1>QRcode Reader test</h1>
    <h2>QRcodeの値：{{ value }}</h2>
    <button @click="handleButton">QRcode読み取り</button>
    <!-- <div v-if="isQrcode" class="qr">
      <qrcode-stream @detect="onDetect"></qrcode-stream>
    </div> -->
    <!-- <div>
      <qrcode-drop-zone @detect="onDetect" class="drop"
        >ドラッグ&ドロップ</qrcode-drop-zone
      >
    </div> -->

    <!-- <div class="capture">
      <qrcode-capture @detect="onDetect"></qrcode-capture>
    </div> -->
  </div>
</template>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.drop {
  width: 300px;
  height: 200px;
  border: solid red 5px;
  margin: 30px;
}

.qr {
  width: 250px;
  height: 250px;
  border: solid 3px green;
}

button {
  font-size: 15px;
  border: none;
  border-radius: 15px;
  background-color: aqua;
  padding: 15px;
  margin: 30px;
}

.capture {
  margin: 10px;
}
</style>
