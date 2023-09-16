<template>
  <div>
    <button @click="doclick">{{count}}</button>
    <div class="a">
      <p>{{word}}</p>
    </div>
  </div>
</template>
<script lang="ts" setup>
import {ref, computed } from 'vue';
let num=0
const count=ref(num)
function doclick(){
  count.value++
}
const word = computed(() => {
  return count.value==0?'我木得了':(count.value%2==0?'我脱单啦':'我又单身啦')
})
</script>
<style lang="less">
button {
  font-weight: bold;
  padding: 10px;
}
div.a{
  background-color: black;
  p{
    color:white;
  }
}
</style>