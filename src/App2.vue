<template>
  <div>
    <div>
      Ref:{{ Man }}
      Count:{{ count }}
    </div>
    <button @click="change">修改</button>
  </div>
  <hr>
  <div>
    <div>
      shallowRef:{{ Man2 }}
      Count:{{ count }}
    </div>
    <button @click="change2">shallowRef修改</button>
  </div>
  <br>
  <ul >
    <li v-for=" item in list.arr">{{ item }}</li>
  </ul>
  <button @click="add">修改</button>
</template>

<script setup lang="ts">
// const Man = {name: '小满'}

import {isRef, reactive, ref, Ref, shallowRef} from "vue";
//ref 深层次响应   shallowRef 浅层次. 不能一块写 会影响shallowRef 造成视图更新


const count = ref(0)
const Man = ref({name: '小满'})


//类型复杂使用
type M = {
  name: string
}
const Man2: Ref<M> = shallowRef({name: '小满'})
const change = () => {
  // Man.value.name = '大满'
  // console.log(Man);
  count.value++
  console.log(isRef(Man))
}
const change2 = () => {
  count.value++
  Man2.value.name = '大满'
  console.log("Line:[39] \t ", Man2)
  Man2.value = {name: '大满  shallowRef'}
  console.log("Line:[41] \t ", Man2)
}


//ref  reactive  都是将变量包装成响应式
//ref 支持所有类型  reactive 引用类型  Array Object Map Set
//ref 取值赋值需要加.value  reactive 不需要
//reactive 是一个代理对象 不能直接赋值 否则会破坏响应式对象
//解决方案  数据可以用push 加解构  或者 用对象 加一个属性  直接修改属性的value
type reactiveType = {
  name: string,
  age: number
}
const form = reactive<reactiveType>({
  name: '小满',
  age: 13,
})

type ListType = {
  arr: string[]
};
const list = reactive<ListType>({
  arr: []
})

const add = () => {
  setTimeout(() => {
    let items = Math.random();
    list.arr.push(items+'')
    console.log(list);
  }, 500)
}


</script>

<style scoped>

</style>
