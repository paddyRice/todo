<template lang="html">
    <footer class="footer" style="">
        <span class="todo-count"><strong>{{todosLeft}}</strong> items left</span>
        <ul class="filters">
            <li><a href="" :class="{selected:filter=='all'}" @click.prevent="setFilter('all')">all</a></li>
            <li><a href="" :class="{selected:filter=='active'}" @click.prevent="setFilter('active')">active</a></li>
            <li><a href="" :class="{selected:filter=='completed'}" @click.prevent="setFilter('completed')">completed</a></li>
        </ul>
        <button class="clear-completed" v-show="completed"
         @click="clearCompleted"
        >clear completed</button>
    </footer>
</template>

<script>
export default {
    props : {
        filter : {
            type : String,
            required : true
        },
        todosLeft : {
            type : Number,
            required : true
        },
        completed:{
            type : Number,
            required : true
        }
    },
    methods : {
        clearCompleted(){
            console.log('aaa');
            this.$emit('clearCompleted');
        },
        setFilter(filter){
            this.$emit('setFilter',filter);
            // this.filter = filter; //不可以的
        }
    }
}
</script>

<style lang="css">
</style>
