<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const editing = ref(false)
const items = ref([
  // { id: 1, label: '10 party hats' },
  // { id: 2, label: '2 board games' },
  // { id: 3, label: '20 cups' },
])
const newItem = ref('')
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value })
  newItem.value = ''
}
const doEdit = (e) => {
  editing.value = e
  newItem.value = ''
}
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">Add Item</button>
  </div>
  <form class="add-item-form" @submit.prevent="saveItem" v-if="editing">
    <input v-model.trim="newItem" type="text" placeholder="Add an item..." />
    <label>
      <input type="checkbox" v-model="newItemHighPriority" />
      Priority
    </label>
    <button class="btn btn-primary" :disabled="newItem.length === 0">Save item</button>
  </form>
  <ul>
    <li v-for="item in items" :key="item.id">{{ item.label }}</li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>
