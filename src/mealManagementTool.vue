<script setup>
import { ref } from 'vue'

const drinksData = ref([
  {
    item: '珍珠奶茶',
    des: '香濃奶茶搭配QQ珍珠',
    price: '50',
    inventory: 20
  },
  {
    item: '冬瓜檸檬',
    des: '清新冬瓜配上新鮮檸檬',
    price: '45',
    inventory: 18
  },
  {
    item: '翡翠檸檬',
    des: '綠茶與檸檬的完美結合',
    price: '55',
    inventory: 34
  },
  {
    item: '四季春茶',
    des: '香醇四季春茶，回甘無比',
    price: '45',
    inventory: 10
  },
  {
    item: '阿薩姆奶茶',
    des: '阿薩姆紅茶搭配香醇鮮奶',
    price: '50',
    inventory: 25
  },
  {
    item: '檸檬冰茶',
    des: '檸檬與冰茶的清新組合',
    price: '45',
    inventory: 20
  },
  {
    item: '芒果綠茶',
    des: '芒果與綠茶的獨特風味',
    price: '55',
    inventory: 18
  },
  {
    item: '抹茶拿鐵',
    des: '抹茶與鮮奶的絕配',
    price: '60',
    inventory: 20
  }
])
const dataSort = ref(['品項', '描述', '價格', '庫存', '編輯品項'])
const tempData = ref(['', ''])

const changeInventory = (fn, index) => {
  //   console.log(num)
  if (fn === 'minor') drinksData.value[index].inventory--
  else if (fn === 'add') drinksData.value[index].inventory++
}

const editMode = (index) => {
  let editArea = document.querySelector('.editArea')
  // console.log(editArea)
  editArea.classList.remove('d-none')
  tempData.value[0] = index
  tempData.value[1] = drinksData.value[index].item
  console.log(tempData[1].value)
}

const revise = () => {
  let index = tempData.value[0]
  drinksData.value[index].item = tempData.value[1]
  tempData.value[0] = ''
  tempData.value[1] = ''
}
const cancelEdit = () => {
  tempData.value[0] = ''
  tempData.value[1] = ''
}
</script>

<template>
  <div class="container">
    <h2 class="mt-3">餐點管理工具</h2>
    <table class="table table-striped table-hover">
      <thead>
        <tr class="table-secondary">
          <th v-for="(data, index) in dataSort" :key="index" class="text-center">{{ data }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(drink, index) in drinksData" :key="index">
          <td>{{ drink.item }}</td>
          <td>{{ drink.des }}</td>
          <td>{{ drink.price }}</td>
          <td class="d-flex justify-content-between align-items-center">
            <button type="button" class="btn btn-primary" @click="changeInventory('minor', index)">
              -
            </button>
            <!-- <input type="text" v-model="drink.inventory" /> -->
            <p class="mx-2 my-0">{{ drink.inventory }}</p>
            <button type="button" class="btn btn-primary" @click="changeInventory('add', index)">
              +
            </button>
          </td>
          <td>
            <button type="button" class="btn btn-danger" @click="editMode(index)">編輯</button>
          </td>
        </tr>
      </tbody>
    </table>

    <hr />
    <div class="editArea d-none">
      <input type="text" v-model="tempData[1]" placeholder="請點擊想要編輯的品項" />
      <button type="button" class="btn btn-warning ms-3" @click="revise()">確認修改</button>
      <button type="button" class="btn btn-danger ms-3" @click="cancelEdit()">取消修改</button>
    </div>
  </div>
</template>
