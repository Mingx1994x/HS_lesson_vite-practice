<script setup>
import { ref } from 'vue'
const num = ref(0)
function clickMe() {
  num.value++
}
</script>

<template>
  <div class="test">
    {{ num }}
    <button type="button" v-on:click="clickMe" class="count-btn">click me</button>
  </div>
</template>

<style>
.count-btn {
  border: 0;
  border-radius: 5px;
  background-color: orange;
}
</style>
