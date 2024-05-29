<script setup lang="ts">
import { ref } from 'vue';
import Tree from './components/Tree.vue';

const node = ref(null);
const finalNode = ref(null);

const listTree = ref([
  {
    id: 0,
    name: 'root',
    children: [
      {
        id: 1,
        name: 'child 1',
        children: [
          {
            id: 5,
            name: 'child 5',
            children: [
              {
                id: 6,
                name: 'child 6',
                children: []
              }
            ]
          }
        ]
      },
      {
        id: 2,
        name: 'child 2',
        children: [
          {
            id: 3,
            name: 'child 3',
            children: []
          },
          {
            id: 4,
            name: 'child 4',
            children: []
          }
        ]
      }
    ]
  }
])

function findAndRemoveNode(tree: any, nodeId: any): null | any {
  if (!tree.children) return null;

  for (let i = 0; i < tree.children.length; i++) {
    if (tree.children[i].id === nodeId) {
      return tree.children.splice(i, 1)[0]; // Remove and return the node
    } else {
      const result = findAndRemoveNode(tree.children[i], nodeId);
      if (result) return result;
    }
  }
  return null;
};

function findNode(tree: any, nodeId: any): null | any {
  if (tree.id === nodeId) {
    return tree;
  }
  if (!tree.children) return null;

  for (let i = 0; i < tree.children.length; i++) {
    const result = findNode(tree.children[i], nodeId);
    if (result) return result;
  }
  return null;
}

function rebuild() {
  console.log(node.value)
  console.log(finalNode.value)
  if ((!node.value || !finalNode.value) || node.value.id === finalNode.value.id) {
    return;
  }

  const searchedNode = findAndRemoveNode(listTree.value[0], node.value.id);
  if (!searchedNode) return;

  const parent = findNode(listTree.value[0], finalNode.value.id);
  console.log(parent)
  if (!parent) return;
  parent.children.push(searchedNode)

  node.value = searchedNode;
  finalNode.value = null;
}

const onDrop = (data: any) => {
  // finalNode.value = data;
  // rebuild()
}

const onDragEnter = (data: any) => {
  finalNode.value = data;
  console.log('dragenter')
  rebuild()
}

const onDragOver = (data: any) => {
  // finalNode.value = data;
  // console.log(finalNode.value)
  // rebuild()
}

const onDrag = (data: any) => {
  // finalNode.value = data;
  // rebuild()
}

const onDragStart = (data: any) => {
  node.value = data;
}
</script>

<template>
  <Tree 
    :treeList="listTree" 
    @tree:drop='onDrop' 
    @tree:dragStart="onDragStart"
    @tree:dragEnter="onDragEnter"
    @tree:dragOver="onDragOver"
    @tree:drag="onDrag"
  ></Tree>
</template>

<style scoped>
</style>
