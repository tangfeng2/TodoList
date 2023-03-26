<template>
    <p class="todo-item" :class="[todo.completed ? 'is-completed':'']" >
        <input type="checkbox" :checked="todo.completed" @change="markCompleted"/>
        {{ todo.title }}
        <button class="del-btn" @click="deleteItem">Delete</button>
    </p>

</template>
<script>
// import { ref } from 'vue'
export default {
    name: 'TodoItem',
    props: ['todo'],
    setup(props, context) {
        const markCompleted = () => {
            context.emit('item-completed', props.todo.id)
        }
        const deleteItem = () => {
            context.emit('item-delete', props.todo.id)
        }
        return {
            deleteItem,
            markCompleted
        }
    }
}
</script>
<style scoped>
.todo-item {
    background: #f4f4f4;
    padding: 10px;
    margin: 0;
    border-bottom: 1px #ccc dotted;
}
.is-completed {
    text-decoration: line-through;
}
.del-btn {
    background: #ff0000;
    color: #fff;
    border: none;
    cursor: pointer;
    float: right;
}
</style>