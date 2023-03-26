<template>
    <AddTodo @addTodo="addTodo" />
    <TodoItem v-for="(todo, index) in todos" :key="index" :todo="todo" @itemCompleted="markCompleted" @itemDelete="deleteTodo" />

</template>
<script>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
import axios from 'axios'
export default {
    name: 'Todos',
    components: {
        TodoItem,
        AddTodo
    },
    setup() {
        const data = JSON.parse(localStorage.getItem('todos'))
        const todos = data || ref([])
        // const getAllTodos = async () => {
        //     try {
        //         const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        //         todos.value = res.data
        //     } catch (e) {
        //         console.error(e)
        //     }
        // }
        // getAllTodos()

        const markCompleted = id => {
            todos.value = todos.value.map(todo => {
                if (todo.id == id) todo.completed = !todo.completed
                return todo
            })
            localStorage.setItem('todos', JSON.stringify(todos.value))
        }

        const deleteTodo = async id => {
            try {
                // await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id)
                localStorage.setItem('todos', JSON.stringify(todos.value))
            } catch (e) {
                console.error(e)
            }
            
        }
        const addTodo = async newTodo => {
            try {
                // const res = await axios.post('https://jsonplaceholder.typicode.com/todos/', newTodo)
                
                todos.value.push(newTodo)
                localStorage.setItem('todos', JSON.stringify(todos.value))
            } catch (e) {
                console.error(e)
            }
            
        }


        return {
            markCompleted,
            deleteTodo,
            todos,
            addTodo
            
        }
    }
}
</script>
<style scoped>
    
</style>