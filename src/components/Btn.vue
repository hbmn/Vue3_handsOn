<script setup lang="ts">
import { ref } from "vue";
const bgColor = ref("bgc");
</script>

<template>
  <a class="btn" v-bind:class="bgColor" href="#">
    <slot>デフォルト</slot>
  </a>
</template>

<style scoped lang="scss">
.btn {
  background-color: green;
  border-radius: 8px;
  color: #fff;
  padding: 10px 20px;
  display: inline-block;
  text-align: center;
  width: 100px;
  font-weight: bold;
  text-decoration: none;
}

.btn:hover {
  opacity: 0.7;
}

.bgc {
  background-color: darkblue;
}
</style>
