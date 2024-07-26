<template>
    <div class="todo-footer" v-show="total">
        <label>
            <input type="checkbox" v-model="isAll"/>
        </label>
        <span>
            <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps(['todos', 'checkAllTodo', 'clearAllTodo']);

const total = computed(() => props.todos.length);

const doneTotal = computed(() => {
    return props.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0);
});

const isAll = computed({
    get: () => doneTotal.value === total.value && total.value > 0,
    set: (value) => {
         props.checkAllTodo(value);
    }
});

const clearAll = () => {
    props.clearAllTodo();
};
</script>

 
 <style scoped>
    /*footer*/
    .todo-footer {
        height: 40px;
        line-height: 40px;
        padding-left: 6px;
        margin-top: 5px;
    }
 
    .todo-footer label {
        display: inline-block;
        margin-right: 20px;
        cursor: pointer;
    }
 
    .todo-footer label input {
        position: relative;
        top: -1px;
        vertical-align: middle;
        margin-right: 5px;
    }
 
    .todo-footer button {
        float: right;
        margin-top: 5px;
    }
 </style>
 