<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const editing = ref(false)
const items = ref([
  { id: 1, label: '10 party hats', purchased: true, highPriority: false },
  { id: 2, label: '2 board games', purchased: true, highPriority: false },
  { id: 3, label: '20 cups', purchased: false, highPriority: true },
])
const newItem = ref('')
const newItemHighPriority = ref(false)
const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    highPriority: newItemHighPriority.value,
  })
  newItem.value = ''
  newItemHighPriority.value = ''
}
const doEdit = (e) => {
  editing.value = e
  newItem.value = ''
  newItemHighPriority.value = ''
}
const togglePurchased = (item) => {
  item.purchased = !item.purchased
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
    <li
      v-for="item in items"
      @click="togglePurchased(item)"
      :key="item.id"
      :class="{ strikeout: item.purchased, priority: item.highPriority }"
    >
      {{ item.label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to see here</p>
</template>
