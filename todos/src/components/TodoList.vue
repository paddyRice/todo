<template lang="html">
    <section class="main" style="">
        <input type="checkbox" class="toggle-all" :checked="allChecked" @click="toggleAll">
        <ul class="todo-list">
            <Todo v-for="(todo,index) in todos" key="index" :todo="todo"
                @deleteTodo="deleteTodo" @toggleTodo="toggleTodo"
                @editTodo="editTodo"
            ></Todo>
        </ul>
    </section>
</template>

<script>
//引入Todo组件
import Todo from './Todo'
export default {
    props : {
        todos : {
            type : Array,
            required : true
        },
        allChecked : {
            type : Boolean,
            required : true
        }
    },
    methods : {
        deleteTodo(todo){
            this.$emit('deleteTodo',todo);
        },
        toggleTodo(todo){
            this.$emit('toggleTodo',todo);
        },
        toggleAll(e){
            this.$emit('toggleAll',e.target.checked);
        },
        editTodo(todo,text){
            this.$emit('editTodo',todo,text);
        }
    },
    components : {
        Todo
    }
}
</script>

<style lang="css">
</style>
