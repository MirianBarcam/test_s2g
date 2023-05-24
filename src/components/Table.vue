<script setup>
const props = defineProps(['dataTable', 'headersTable', 'dataToEvaluate'])
</script>

<template>
  <div class="container-table">
    <table>
      <thead>
        <tr>
          <th v-for="title in headersTable">
            {{ title }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="data in dataTable">
          <td v-for="user in data" :class="data[dataToEvaluate] ? 'available' : 'not-available'">
            {{ user }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.container-table {
  width: 100%;
  overflow-y: scroll;
  height: 20rem;
}
.available {
  background-color: #85c5a83c;
}

.not-available {
  background-color: rgba(224, 97, 97, 0.21);
}
body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}

table {
  background-color: #fff;
  width: 100%;
  border-spacing: 0px;
}

th {
  background-color: #34495e;
  color: #f9f9f9;
  position: sticky;
  top: 0;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  height: 2rem;
  text-align: center;
  border: 1px solid white;
}
</style>
