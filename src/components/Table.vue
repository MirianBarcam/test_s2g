<script setup>
import { ref } from 'vue'

//import { useGetData } from '@/composables/getData'

//const { data, getData, loading } = useGetData()
const datatable = ref()
//console.log(data.results)

//getData(' https://s2grupo-b4529-default-rtdb.europe-west1.firebasedatabase.app/users.json')
fetch('https://s2grupo-b4529-default-rtdb.europe-west1.firebasedatabase.app/users.json')
  .then((res) => res.json())
  .then((data) => (datatable.value = data))
  .catch((e) => console.log(e))
  .finally(() => {
    loading.value = false
  })
console.log('datos:', datatable.value)
</script>

<template>
  <div class="container-table">
    tabla
    <!-- <table>
      <thead>
        <tr>
          
          <th
            v-for="campo in data.results"
            @click="sortBy(campo)"
            :class="{ active: sortKey == campo }"
          >
            {{ campo | capitalize }}
            <span class="arrow" :class="sortOrders[campo] > 0 ? 'asc' : 'dsc'"> </span>
          </th>
        </tr>
      </thead>
    </table> -->
  </div>
</template>

<style>
.container-table {
  border: 1px solid #ddd;
  height: 80vh;
  overflow-y: scroll;
}
</style>
