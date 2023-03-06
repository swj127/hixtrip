<script setup lang="ts">
import tree from './components/tree.vue'
import tables from './components/table.vue'
import { onMounted, ref } from 'vue'
import userApi from './api/user'
import orgApi from './api/org'

let user = ref<any>()
let org = ref<any>()
let handleNodeClickId = '' // 用于记录是否 是全组织

const handleNodeClick = (data: any) => {
  handleNodeClickId = data.id == 'undefined' ? '' : data.id
  if (!data.id) {
    getUserApi()
    return
  }
  user.value = [data]
}
const getUserApi = () => {
  userApi.query({}).then(res => (user.value = res))
}
onMounted(() => {
  getUserApi()
  orgApi.query().then(res => (org.value = res))
})

const input = ref('')
const seach = () => {
  if (!input.value) {
    if (handleNodeClickId) return
    getUserApi()
    return
  }
  let data = user.value.filter((item: any) => {
    return item.name.indexOf(input.value) != -1
  })
  user.value = data
}
</script>

<template>
  <div class="flex">
    <tree :data="org" @handleNodeClick="handleNodeClick" />
    <div>
      <div class="flex">
        <el-input v-model="input" placeholder="请输入搜索内容" clearable />
        <el-button type="primary" @click="seach">搜索</el-button>
      </div>
      <tables :tableData="user" />
    </div>
  </div>
</template>

<style scoped>
.flex {
  display: flex;
}
</style>
