<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="name" label="姓名" width="180" />
    <el-table-column prop="id" label="用户名" width="250" />
  </el-table>
</template>

<script lang="ts" setup>
const props = defineProps({
  tableData: {
      type: Array,
      default: []
    }
  }) 



</script>
