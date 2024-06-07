<script setup>
import { ref } from 'vue'

const header = ref("Todo List")
const items = ref([
    { id: 1, time: "08:00", label: "Wake Up",  isHighPriority: false, isDone: true  },
    { id: 2, time: "12:00", label: "Lunch",    isHighPriority: false, isDone: false },
    { id: 3, time: "14:30", label: "Call Mom", isHighPriority: true,  isDone: false },
])
const newItemTime = ref("")
const newItemLabel = ref("")
const newItemHighPriority = ref(false)
const isEditing = ref(false)
const addNewItem = () => {
    items.value.push({ id: items.value.length+1, time: newItemTime.value, label: newItemLabel.value, isHighPriority: newItemHighPriority.value }),
    newItemTime.value = "",
    newItemLabel.value = "",
    newItemHighPriority.value = false
}
const doEdit = (e) => {
    isEditing.value = e,
    newItemTime.value = "",
    newItemLabel.value = "",
    newItemHighPriority.value = false
}
const toggleDone = (item) => {
    item.isDone = !item.isDone
}
</script>

<template>
    <div class="todo-list-container">
        <div class="todo-list-header">
            <h1>{{ header.toLocaleUpperCase() }}</h1>
            <form 
                class="todo-list-add-item-form" 
                v-if="isEditing" 
                @submit.prevent="addNewItem" 
            >
                <div class="todo-list-form-inputs">
                    <input v-model="newItemTime" type="time" required>
                    <input v-model="newItemLabel" type="text" placeholder="Add an item" required>
                    <input v-model="newItemHighPriority" type="checkbox">
                </div>
                <div class="todo-list-form-buttons">
                    <button :disabled="newItemLabel.length === 0 || newItemTime.length === 0" @click="submit">
                        Save
                    </button>
                    <button v-if="isEditing" @click="doEdit(false)">
                        Cancel
                    </button>
                </div>
            </form>
            <button class="todo-list-add" v-else @click="doEdit(true)">
                Add
            </button>
        </div>
        <div class="todo-list-list">
            <ul>
                <li 
                    v-for="item in items" 
                    :key="item.id"
                    :class="{ 'todo-list-item-done': item.isDone, 'todo-list-item-high-priority': item.isHighPriority }" 
                    @click="toggleDone(item)" 
                >
                    <span class="todo-list-item-time">{{ item.time }}</span>
                    <span class="todo-list-item-label">{{ item.label }}</span>
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    .todo-list-header {
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    h1 {
        margin-top: 2rem;
    }

    .todo-list-form-inputs input {
        margin: 1rem;
    }

    .todo-list-form-buttons {
        display: flex;
        justify-content: center;
    }

    button {
        width: 6rem;
        height: 2rem;
        margin: 0 1rem;
    }

    .todo-list-list {
        width: 60vw;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    ul {
        margin: 1rem;
        outline: dashed 1px black;
    }

    li {
        list-style-type: none;
        margin: 1rem;
    }

    .todo-list-item-done {
        text-decoration: line-through;
    }

    .todo-list-item-high-priority {
        color: chocolate;
    }

    span {
        margin: 0 1rem;
    }

    .todo-list-add {
        margin-top: 1rem;
    }
</style>
