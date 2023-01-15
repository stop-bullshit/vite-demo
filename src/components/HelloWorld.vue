<script setup lang='ts'>
import {ref} from 'vue'

//TS专用
const props = withDefaults(defineProps<{
  msg: string
  greetingMsg?: string
}>(), {
  msg: "这是默认Msg",
  greetingMsg: '你好'
})

console.log(props.msg)
//非TS
// const props = defineProps({
//   msg:{
//     type:String,
//     default:'这是属性的默认值'
//   }
// })

// 非TS
// const emits = defineEmits(['on-click']);

// TS
const emits = defineEmits<{
  (e: 'on-click', name: string): void
}>()

const send = () => {
  emits('on-click', '这是name参数')
}

</script>

<template>
  <h1>{{ greetingMsg }}</h1>
  <h2>{{ msg }}</h2>
  <button @click='send'>send</button>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
