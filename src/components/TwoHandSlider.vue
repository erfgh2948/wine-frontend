<template>
  <div class="sliderContainter">
    <div class="slider"></div>
    <div class="progress"></div>
    <div class="range-input">

      <input type="range" class="range-min" v-model="minVal" min="0" max="100000" step="10000" @mousemove="sliderValLeft"
        @mouseup="sliderValLeftSaparate">
      <input type="range" class="range-max" v-model="maxVal" min="0" max="100000" step="10000" @mousemove="sliderValRight"
        @mouseup.stop="sliderValRightSaparate">

    </div>    
    <div class="priceBetween" >
      <p>\ {{ minVal }}</p>
      <p>\ {{ maxVal }}</p>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue';
let minVal = ref(0);
let maxVal = ref(100000);

const sliderValLeft = (e) => {
  const progress = document.querySelector(".progress");
  console.log(e.target.className)
  if (maxVal.value == minVal.value ) {
    minVal.value = maxVal.value
    e.preventDefault();
  }
  if (e.target.className == "range-min") {
    progress.style.left = (minVal.value / 100000) * 100 + "%";
  }
}
const sliderValLeftSaparate=()=>{
  const progress = document.querySelector(".progress");
  if(minVal.value==maxVal.value)
  minVal.value=maxVal.value-10000
  progress.style.left = (minVal.value / 100000) * 100 + "%";
}
const sliderValRight = (e) => {
  const progress = document.querySelector(".progress");
  console.log(e.target.className)
  if (minVal.value >= maxVal.value ) {
    maxVal.value = minVal.value
    e.preventDefault();
  }
  if (e.target.className == "range-max") {
    progress.style.right = 100-((maxVal.value / 100000) * 100)+ "%";
  }
  
}
const sliderValRightSaparate = ()=>{
  const progress = document.querySelector(".progress");
  if(minVal.value===maxVal.value)
  maxVal.value=parseInt(minVal.value)+10000
  progress.style.right = 100-((maxVal.value / 100000) * 100) + "%";
 // console.log(maxVal)
}

</script>

<style scoped>
*{margin:0;padding:0;box-sizing: border-box;}

.sliderContainter{
  position:relative;
  width:100%; height:50px;
  margin-top:30px;
}
.slider{
  position:absolute;
  top:-3px;left:0%;right:0%;
  height:8px;border-radius: 5px;
  background-color: #f4f4f4;
}
.progress{
  height:8px;
  position:absolute;
  top:-3px;left:0%;right:0%;
  border-radius: 5px;
  background-color: #c70039;
  
}
.range-input{
  position:relative
}
/* ???????????? ???????????? */

/* min-max ????????? ?????? ??? ?????????. */
.range-input input{
  position:absolute;
  top:-5px;
  height:10px;
  width:100%;
  background:none;
  pointer-events: none;
  background-color: none;
  appearance: none;
}
/* ??? ????????? */
input[type="range"]::-webkit-slider-thumb{
  height:18px;width:18px;
  background: #fff; 
  pointer-events: auto;
  appearance: none;
  border:1px solid #c70039;
  border-radius: 50%;
}
/* input[type="range"]::after{
  height:15px;width:15px;
  content:'';
  color:green;
} */

/* ?????? */
.priceBetween {
  display:flex; justify-content:space-between;
  font-family:none;
  padding-top:7px;  
  }
</style>