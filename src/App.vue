<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  { id: 1, label: '10 party hats' },
  { id: 2, label: '2 board games' },
  { id: 3, label: '20 cups' },
])
const newItem = ref('')
const newItemPriority = ref('low')
</script>

<template>
  <h1>{{ header }}</h1>
  <input v-model.trim="newItem" type="text" placeholder="Add an item..." />
  Priority:
  <label>
    <input type="radio" v-model="newItemPriority" value="low" />
    Low
  </label>
  <label>
    <input type="radio" v-model="newItemPriority" value="high" />
    High
  </label>
  <ul>
    <li v-for="item in items" :key="item.id">{{ item.label }}></li>
  </ul>
</template>
