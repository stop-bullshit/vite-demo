<template>
  <div>
<!--    <hello-world :msg='helloMessage'></hello-world>-->
<!--    <hello-world></hello-world>-->
    <hello-world @on-click='getName'></hello-world>
  </div>
</template>

<script setup lang='ts'>
import HelloWorld from "./components/HelloWorld.vue";

const helloMessage = "父级message"

const getName = (name:string) => {
  console.log("父组件获得参数:",name)
}

</script>

<style scoped>

</style>
