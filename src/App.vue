<template>
  <div>
    {{
      a.map(v => ({num: v}))
    }}
  </div>
  <div v-text="b">
  </div>
  <div @click="parent">
    <button @click="xxx">Click
    </button>
  </div>

  <button @[event]="xxx">Click2
  </button>

  <div :id="id" :style="style">
    {{ id }}
  </div>


  <div>
    <input v-model="modela" type="text">
    <div>{{ modela }}</div>

    <div :key='index' v-for="(item,index) in arr">
      {{ index }}-{{ item }}
    </div>

    <!--    //只渲染一次-->
    <div v-once>
      {{ modela }}
    </div>
  </div>
</template>

<script setup lang="ts">
import {ref} from "vue";

const arr: string[] = ["123", '456']


const style = {
  color: 'red',
  border: '5px solid #ccc'
}
const id: string = '123'
const a: number[] = [1, 2, 3, 4, 5];
const modela = ref<String>("hello");
const b: string = 'akshdlkashdahsld'

let count = ref<number>(0)
//动态事件切换
const event = 'click'
const parent = () => {
  console.log("我是父级")
}
const xxx = () => {
  console.log("点击了XXX")
}
</script>

<style scoped lang="less">

</style>
