<script setup>
const props = defineProps(['dataTable', 'headersTable'])
</script>

<template>
  <div class="container-table">
    <table class="container-table">
      <thead>
        <tr>
          <th v-for="title in headersTable">
            {{ title }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="data in dataTable">
          <td v-for="user in data" :class="data.available ? 'available' : 'not-available'">
            {{ user }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style>
.available {
  background-color: #85c5a83c;
}

.not-available {
  background-color: rgba(224, 97, 97, 0.21);
}

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
  border: 2px solid #0a2217;
  background-color: #fff;
}

th {
  background-color: #34495e;
  color: #f9f9f9;
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
