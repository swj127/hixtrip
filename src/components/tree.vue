<template>
  <el-tree :props="props" :load="loadNode" lazy @node-click="handleNodeClick" />
</template>

<script lang="ts" setup>
import type Node from 'element-plus/es/components/tree/src/model/node'

interface Tree {
  name: string
  leaf?: boolean
}

const props = {
  label: 'name',
  children: 'zones',
  isLeaf: 'leaf'
}
const prop = defineProps({
  data: {
    type: Array,
    default: []
  }
})
const emit = defineEmits(['handleNodeClick'])

const loadNode = (node: Node, resolve: (data: Tree[]) => void) => {
  if (node.level === 0) {
    return resolve([{ name: 'region' }])
  }
  if (node.level > 1) return resolve([])

  setTimeout(() => {
    let data: any = prop.data
    resolve(data)
  }, 500)
}
const handleNodeClick = (data: Tree) => {
  emit('handleNodeClick', data)
}

</script>
