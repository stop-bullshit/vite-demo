<template>
  <div>
    <input v-model='firstName' type='text'>
    <input style='margin-left: 20px' v-model='lastName' type='text'>
  </div>
  {{ firstName }}--{{ lastName }}!
  <br>
  <span>{{ name }}</span>
  <br style='margin-top: 100px'>
  <div>
    <table>
      <button @click='add'>新增</button>
      <thead>
      <tr>
        <th>名称</th>
        <th>数量</th>
        <th>单价</th>
        <th>操作</th>
      </tr>
      </thead>
      <tbody>
      <tr :key='index' v-for='(item ,index) in data'>
        <td>{{ item.name }}</td>
        <td style='width: 300px'>
          <button @click='addOrSub(item,true)'>+</button>
          <span style='width: 100px'> {{ item.num }}</span>
          <button @click='addOrSub(item,false)'>-</button>
        </td>
        <td>{{ item.price }}</td>
        <td style='align-items: center'>
          <button @click='del(index)'> 删除</button>
        </td>
      </tr>
      </tbody>
      <tfoot>

      <tr>
        <th></th>
        <th></th>
        <th></th>
        <th>总价: {{ $total }}</th>
      </tr>
      </tfoot>
    </table>
  </div>
</template>

<script setup lang='ts'>
import {computed, reactive, ref} from "vue";

let firstName = ref('')
let lastName = ref('')

const name = computed(() => {
  return firstName.value + '---' + lastName.value
})

type Shop = {
  name: string,
  num: number,
  price: number
}

let $total = ref(0)
// const total = () => {
//   $total.value = data.reduce((prev, next) => {
//     return prev + (next.num * next.price)
//   }, 0)
// }
const data = reactive<Shop[]>([
  {name: 'h', num: 25, price: 100},
  {name: 'w', num: 30, price: 200},
  {name: 's', num: 30, price: 300},
  {name: 'z', num: 30, price: 50},
]);
// total()
const randomString = (length: number): string => {
  length = length || 32;
  let t = "ABCDEFGHJKMNPQRSTWXYZabcdefhijkmnprstwxyz",
      a = t.length,
      n = "";
  for (let i = 0; i < length; i++) n += t.charAt(Math.floor(Math.random() * a));
  return n
}
const add = () => {
  data.push({
    name: randomString(1),
    num: Math.ceil(Math.random() * 10),
    price: Math.round(Math.random() * 100),
  })
  // total()
}
const del = (index: number) => {
  console.log('del')
  data.splice(index, 1)
  // total()
}


const addOrSub = (item: Shop, action: boolean) => {
  console.log(item);
  if (item.num > 1 && action) {
  }
  if (item.num < 99 && !action) {
    item.num--
  }
  // total()
}


$total = computed<number>(() => {
  return data.reduce((prev, next) => {
    return prev + (next.num * next.price)
  }, 0)
})
</script>

<style scoped lang='less'>
td {
  width: 100px;
}
</style>
