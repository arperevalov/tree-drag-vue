<script setup lang="ts">
import Tree from './Tree.vue';

defineProps<{ item: any }>()
</script>

<template>
  <li>
    <span draggable="true">
      {{ item.name }}
    </span>
    <Tree :treeList="item.children"
      @tree:drop="$emit('tree:drop', $event)"
      @tree:dragStart="$emit('tree:dragStart', $event)"
      @tree:dragEnter="$emit('tree:dragEnter', $event)"
      @tree:dragOver="$emit('tree:dragOver', $event)"
      @tree:drag="$emit('tree:drag', $event)"></Tree>
  </li>
</template>

<style scoped>
</style>
