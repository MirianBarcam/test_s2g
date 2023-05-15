<script setup>
import { ref } from 'vue'
import { format } from 'date-fns'
import es from 'date-fns/locale/es'
window.locale = es
import { useGetData } from '../composable/GetData'

//const { data, getData, loading } = useGetData()
const dataTable = ref([{}])
const headerTable = ref(['Name', 'Age', 'Available', 'Last Login'])
const listado = ref([])

// getData('https://s2grupo-b4529-default-rtdb.europe-west1.firebasedatabase.app/users.json')
// console.log(data.value.results)
fetch('https://s2grupo-b4529-default-rtdb.europe-west1.firebasedatabase.app/users.json')
  .then((res) => res.json())
  .then((data) => {
    dataTable.value = data
  })
  .catch((e) => console.log(e))
  .finally(() => {
    loading.value = false
    if (dataTable.value) listado.value = dataFormat(dataTable.value)
    console.log(dataTable.value)
  })

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
</script>

<template>
  <div v-if="loading">loading...</div>
  <div v-else class="container-table">
    <table class="container-table">
      <thead>
        <tr>
          <th v-for="title in headerTable">
            {{ title }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="data in listado">
          <td v-for="user in data">
            {{ user }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.container-table {
  border: 1px solid #ddd;
  height: 100%;
  width: 100%;
  overflow-y: scroll;
}
body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}

table {
  border: 2px solid #42b983;
  background-color: #fff;
}

th {
  background-color: #42b983;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
  text-align: center;
}
</style>
