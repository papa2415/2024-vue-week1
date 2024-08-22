<script setup>
import { ref } from 'vue'
const editing = ref(false)
const editDrink = ref({})
const drinks = ref([
  { id: 1, name: '珍珠奶茶', description: '香濃奶茶搭配QQ珍珠', price: 50, stock: 20 },
  { id: 2, name: '冬瓜檸檬', description: '清新冬瓜配上新鮮檸檬', price: 45, stock: 18 },
  { id: 3, name: '翡翠檸檬', description: '綠茶與檸檬的完美結合', price: 55, stock: 34 },
  { id: 4, name: '四季春茶', description: '香醇四季春茶，回甘無比', price: 45, stock: 10 },
  { id: 5, name: '阿薩姆奶茶', description: '阿薩姆紅茶搭配香醇鮮奶', price: 50, stock: 25 },
  { id: 6, name: '檸檬冰茶', description: '檸檬與冰茶的清新組合', price: 45, stock: 20 },
  { id: 7, name: '芒果綠茶', description: '芒果與綠茶的獨特風味', price: 55, stock: 18 },
  { id: 8, name: '抹茶拿鐵', description: '抹茶與鮮奶的絕配', price: 60, stock: 20 }
])
const addCart = (drink) => {
  const index = drinks.value.findIndex((item) => item.id === drink.id)
  drinks.value[index].stock++
}
const subCart = (drink) => {
  const index = drinks.value.findIndex((item) => item.id === drink.id)
  drinks.value[index].stock--
}
const edit = (drink) => {
  editing.value = true
  const index = drinks.value.findIndex((item) => item.id === drink.id)
  console.log(drinks.value[index])
  console.log(editDrink.value)
  editDrink.value.id = drinks.value[index].id
  editDrink.value.name = drinks.value[index].name
  editDrink.value.description = drinks.value[index].description
  editDrink.value.price = drinks.value[index].price
  editDrink.value.stock = drinks.value[index].stock
}
const submit = () => {
  const index = drinks.value.findIndex((item) => item.id === editDrink.value.id)
  drinks.value[index].name = editDrink.value.name
  editDrink.value = {}
  editing.value = false
}
</script>

<template>
  <h1>後臺管理</h1>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="drink in drinks" :key="drink.id">
        <td>{{ drink.name }}</td>
        <td>
          <small>{{ drink.description }}</small>
        </td>
        <td>{{ drink.price }}</td>
        <td>
          <button @click="subCart(drink)">-</button>{{ drink.stock
          }}<button @click="addCart(drink)">+</button>
        </td>
        <td><button @click="edit(drink)">編輯</button></td>
      </tr>
    </tbody>
  </table>
  <input v-if="editing" type="text" v-model="editDrink.name" />
  <button v-if="editing" @click="submit">送出</button>
</template>

<style scoped></style>
