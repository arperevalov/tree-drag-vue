<script setup lang="ts">
import { ref } from 'vue';
import TreeElement from './TreeElement.vue';

defineProps<{ treeList: any }>()

const emit = defineEmits();

const startX = ref(0);
const delta = ref(0);

const onDragStart = (e) => {
  emit('tree:dragStart', e)
  // console.log(args);
  // const {clientX} = args[0];
  // startX.value = clientX;
}
const onDragEnter = (e) => {
  emit('tree:dragEnter', e)
  // console.log(args);
  // const {clientX} = args[0];
  // startX.value = clientX;
}
const onDragOver = (e) => {
  emit('tree:dragEnter', e)
  // console.log(args);
  // const {clientX} = args[0];
  // startX.value = clientX;
}

const onDrag = (e: any) => {
  emit('tree:drag', e)
  // const {clientX} = e;
  // delta.value = clientX - startX.value;
}

const onDragEnd = (e: any) => {
  // console.log(e.currentTarget)
  // console.log(e.movementX)
}

const onDrop = (e: any) => {
  emit('tree:drop', e)
  // console.log(e.movementX)
}
</script>

<template>
  {{ startX }}
  {{ delta }}
  <ul>
    <TreeElement 
      v-for="item in treeList" 
      :item="item"
      @drag="onDrag(item)"
      @dragstart.stop="onDragStart(item)"
      @dragend="onDragEnd(item)"
      @dragover.prevent="onDragOver(item)"
      @dragenter.prevent="onDragEnter(item)"
      @drop.stop="onDrop(item)"
      @tree:dragEnter="$emit('tree:dragEnter', $event)"
      @tree:drop="$emit('tree:drop', $event)"
      @tree:dragStart="$emit('tree:dragStart', $event)"
      @tree:dragOver="$emit('tree:dragOver', $event)"
      @tree:drag="$emit('tree:drag', $event)"
    >
    </TreeElement>
  </ul>
</template>

<style scoped>
</style>
