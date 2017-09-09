<template lang="html">
    <li class="todo" :class="{completed : todo.done, editing : editing}" >
        <div class="view">
            <input type="checkbox" :checked="todo.done" class="toggle"
            @click="toggleTodo(todo)">
            <label @dblclick="editing=true">{{todo.text}}</label>
            <button class="destroy" @click='deleteTodo(todo)'></button>
        </div>
        <input type="text" class="edit" :value="todo.text"
            @keyup.enter="doneEdit(todo,$event)"
            @keyup.esc="cancelEdit"
            @blur="doneEdit(todo,$event)"
        >
    </li>
</template>

<script>
export default {
    data(){
        return {
            editing : false
        }
    },
    props : {
        todo : {
            type : Object,
            required : true
        }
    },
    methods : {
        deleteTodo(todo){
            //向父组件emit事件
            this.$emit('deleteTodo',todo);
        },
        toggleTodo(todo){
            //向父组件emit事件
            this.$emit('toggleTodo',todo);
            //直接操作传递过来的props中的todo (不推荐)
            // this.todo.done = !this.todo.done;
        },
        doneEdit(todo,e){
            console.log(e);
            //需要进行修改操作
            let text = e.target.value.trim();
            //如果text为空，就是删除操作，否则为编辑操作
            console.log(text);
            if (text) {
                this.$emit('editTodo',todo,text);
            } else {
                this.deleteTodo(todo);
            }
            //完成之后，也需要修改editing的值
            this.editing = false;
        },
        cancelEdit(){
            //只需要修改editing的值
            this.editing = false;
        }
    }
}
</script>

<style lang="css">
</style>
