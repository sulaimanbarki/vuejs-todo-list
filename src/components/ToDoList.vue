<template>
    <div class="todo-list">
        <h4 v-show="hasDoneItems">TODO List</h4>
        <div class="item-box">
            <div class="" v-for="item in todoList" :key="item.id">
                <div v-if="!item.isDone" class="item">
                    <div class="left">
                        <input type="checkbox" name="" id="item1" :checked="item.isDone" @click="updateOnCheckBoxTodoList(item.id)">
                        <label for="item1">{{ item.text }}</label>
                    </div>
                    <div class="right">
                        <button>Delete</button>
                    </div>
                </div>
            </div>
        </div>
        <h4 v-show="hasUndoneItems">TODO Completed List</h4>
        <div class="item-box">
            <div class="" v-for="item in todoList" :key="item.id">
                <div v-if="item.isDone" class="item">
                <div class="left">
                    <input type="checkbox" name="" id="item1" :checked="item.isDone" @click="updateOnCheckBoxTodoList(item.id)">
                    <label for="item1">{{ item.text }}</label>
                </div>
                <div class="right">
                    <button @click="deleteItem(item.id)">Delete</button>
                </div>
            </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';

const emits = defineEmits(['updateTodoList', 'deleteItem']);

const updateOnCheckBoxTodoList = (item) => {
    emits('updateTodoList', item);
}

const deleteItem = (itemId) => {
    emits('deleteItem', itemId);
}

const props = defineProps({
    todoList: {
        type: Object,
        required: true
    }
})

// hasUndoneItems computed property
const hasUndoneItems = computed(() => {
    return props.todoList.filter((item) => item.isDone).length > 0;
})

// hasDoneItems computed property
const hasDoneItems = computed(() => {
    return props.todoList.filter((item) => !item.isDone).length > 0;
})

</script>

<style scoped>
.todo-list {
    margin-top: 20px;
}

.todo-list hr {
    margin: 15px auto;
    height: 2px solid black;
    border: 5px solid #E741A2;
    width: 50%;
    border-radius: 3px;
}

.item-box {
    margin-top: 10px;
}


.item {
    background-color: #FEFEFE !important;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 3px 0;
}

.item input {
    display: inline-block;
    margin: 7px;
}

.item button {
    padding: 5px;
    border: 0;
    margin: 4px 4px;
    background-color: #E741A2;
    color: white;
}
</style>