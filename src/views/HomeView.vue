<script setup>
import Square from '../components/Square.vue'
import Table from '../components/Table.vue'
</script>

<template>
  <body class="container">
    <div class="container-left">
      <Square />
    </div>
    <div class="container-right">
      <Table></Table>
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
