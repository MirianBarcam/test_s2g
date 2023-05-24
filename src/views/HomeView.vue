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
const dataToEvaluate = 'available'
const dataFormat = (data) => {
  let userOrderedList = data.map((user) => {
    let userOrdered = {
      name: user.name + ' ' + user.surname,
      age: user.age,
      available: user.available,
      lastlogin: format(new Date(user.last_login * 1000), 'dd-MM-yyyy', { locale: window.locale })
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
      <Table
        :dataTable="dataTable"
        :headersTable="headersTable"
        :dataToEvaluate="dataToEvaluate"
      ></Table>
    </div>
  </body>
</template>

<style>
.container {
  height: auto;
  margin: 0;
  box-sizing: border-box;
  min-height: 0;
  display: flex;
  flex-direction: row;
  flex-grow: 1;
  max-height: 500px;
}

.container-left {
  width: 20rem;
  flex-shrink: 0;
  margin: 1rem;
}

.container-right {
  flex-grow: 1;
  padding-left: 1rem;
  margin: 1rem;
}
</style>
