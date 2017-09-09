<template>
    <header class="header">
        <h1>todos</h1>
            <input type="text" placeholder="what need to be done?" class="new-todo"
                @keyup.enter="addTodo"
            >
    </header>
</template>

<script>
export default {
    methods : {
        addTodo(e){ //e就是事件对象
            // console.log(e.target.value);
            let text = e.target.value.trim(); //获取文本框的值
            if (text) {
                //向父组件emit事件
                this.$emit('addTodo',text);
                //清除文本框的值
                e.target.value = "";
            }
        }
    }
}
</script>

<style>
</style>
