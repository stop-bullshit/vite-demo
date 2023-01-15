<template>
  <div>
    {{ man }}
    <br>
    <hr>
    toRef:{{ like }}
  </div>
  <hr>
  <div>
    <button @click='change'>修改</button>
  </div>
</template>

<script setup lang='ts'>

//toRef 只能修改响应式对象的值,非响应式的视图毫无变化(提取单个属性的值)

import {reactive, toRef} from "vue";

const form = {name: '小满', age: 23, like: 'jk'};

const man = reactive(form)

const like = toRef(man, 'like');
const change = () => {
  man.like = 'lilt'
  console.log(man);

  like.value = 'kaka'
  console.log(man);
}

//toRefs 用于解构reactive的对象,结构出来的都是响应式对象
// toRefs()实现
// const toRefs = <T extends object>(object: T) => {
//   const map: any = {};
//   for (let key in object) {
//     map[key] = toRef(object, key)
//   }
//   return map;
// }
</script>

<style scoped>

</style>
