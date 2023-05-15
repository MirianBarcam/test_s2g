<script setup>
import Square from '../components/Square.vue'
import Table from '../components/Table.vue'

import { ref } from 'vue'
import { format } from 'date-fns'
import es from 'date-fns/locale/es'
window.locale = es
import { useGetData } from '../composable/GetData'

const { getData, data, loading } = useGetData()
const headersTable = ref(['Name', 'Age', 'Available', 'Last Login'])
const dataTable = ref([])
const dataFormat = (arrayData) => {
  let userOrderedList = arrayData.map((user) => {
    let userOrdered = {
      name: user.name + ' ' + user.surname,
      age: user.age,
      available: user.available,
      lastlogin: format(new Date(user.last_login), 'dd-MM-yyyy', { locale: window.locale })
    }
    return userOrdered
  })
  return userOrderedList
}

getData('https://s2grupo-b4529-default-rtdb.europe-west1.firebasedatabase.app/users.json').then(
  () => {
    dataTable.value = dataFormat(data.value)
  }
)
</script>

<template>
  <body class="container">
    <div class="container-left">
      <Square />
    </div>
    <div v-if="loading">loading...</div>
    <div v-else class="container-right">
      <Table :dataTable="dataTable" :headersTable="headersTable"></Table>
    </div>
  </body>
</template>

<style>
.container {
  height: 100%;
  padding: 1.5rem 2rem 1.5rem 2rem;
  display: flex;
  flex-direction: row;
  gap: 1.5rem;
}

.container-left {
  width: 20%;
}

.container-right {
  width: 80%;
}
</style>
