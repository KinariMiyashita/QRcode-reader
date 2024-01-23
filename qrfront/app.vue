<script setup>
import { QrcodeStream, QrcodeDropZone, QrcodeCapture } from 'vue-qrcode-reader';
const value = ref();
const isQrcode = ref(false);

const barcodeTypes = [
  'aztec',
  'code_128',
  'code_39',
  'code_93',
  'codabar',
  'databar',
  'databar_expanded',
  'data_matrix',
  'dx_film_edge',
  'ean_13',
  'ean_8',
  'itf',
  'maxi_code',
  'micro_qr_code',
  'pdf417',
  'qr_code',
  'rm_qr_code',
  'upc_a',
  'upc_e',
  'linear_codes',
  'matrix_codes',
];

const onDetect = (content) => {
  value.value = content[0].rawValue;
};

const handleButton = (content) => {
  isQrcode.value = !isQrcode.value;
};

function paintOutline(detectedCodes, ctx) {
  for (const detectedCode of detectedCodes) {
    const [firstPoint, ...otherPoints] = detectedCode.cornerPoints;

    ctx.strokeStyle = 'red';

    ctx.beginPath();
    ctx.moveTo(firstPoint.x, firstPoint.y);
    for (const { x, y } of otherPoints) {
      ctx.lineTo(x, y);
    }
    ctx.lineTo(firstPoint.x, firstPoint.y);
    ctx.closePath();
    ctx.stroke();
  }
}
</script>
<template>
  <div class="app">
    <h1>QRcode Reader test</h1>
    <h2>QRcodeの値：{{ value }}</h2>
    <button @click="handleButton">QRcode読み取り</button>
    <div v-if="isQrcode" class="qr">
      <qrcode-stream
        @detect="onDetect"
        :track="paintOutline"
        :formats="barcodeTypes"
      ></qrcode-stream>
    </div>
    <div class="capture">
      <qrcode-capture @detect="onDetect"></qrcode-capture>
    </div>
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
