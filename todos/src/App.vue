<template>
    <section class="todoapp">
        <AddTodo @addTodo="addTodo"></AddTodo>
        <TodoList :todos="filteredTodos" :allChecked="allChecked" @deleteTodo="deleteTodo"
        @toggleTodo="toggleTodo" @toggleAll="toggleAll" @editTodo="editTodo"
        ></TodoList>
        <TodoFooter :todosLeft="todosLeft" :completed="completed" :filter="filter"
            @clearCompleted="clearCompleted" @setFilter="setFilter"
        ></TodoFooter>
    </section>
</template>

<script>
import AddTodo from './components/AddTodo'
import TodoList from './components/TodoList'
import TodoFooter from './components/TodoFooter'

export default {
  name: 'app',
  data(){
      return {
          todos : [
              {text : '金榜题名时', done : true},
              {text : '洞房花烛夜', done : false},
              {text : '他乡遇故知', done : false},
          ],
          filter : 'all'
      }
  },
  computed : {
      //获取所有任务的完成情况，如果都完成，返回true，否则返回false
      allChecked(){
          return this.todos.every(todo => todo.done);
      },
      //统计未完成的todos
      todosLeft(){
          return this.todos.filter(todo => !todo.done).length;
      },
      //统计已完成的todos
      completed(){
          return this.todos.filter(todo => todo.done).length;
      },
      //根据filter筛选todos
      filteredTodos(){
          switch(this.filter) {
              case 'all':
                return this.todos;
              case 'active' :
                return this.todos.filter( todo => !todo.done);
              case 'completed':
                return this.todos.filter( todo => todo.done);
              default :
                return ;
          }
      }
  },
  methods : {
      //添加todo
      addTodo(text){ //text就是子组件传递过来的对象
          this.todos.push({
              text,
              done : false
          });
      },
      //删除todo
      deleteTodo(todo) {
          //根据todo查找索引
          let index = this.todos.findIndex( tt => tt===todo );
          this.todos.splice(index,1);
      },
      //切换指定todo的状态
      toggleTodo(todo) {
           let index = this.todos.findIndex( tt => tt===todo );
           this.todos[index].done = !this.todos[index].done;
      },
      //批量切换todos的状态
      toggleAll(done){
          this.todos.forEach( todo => todo.done = done);
      },
      //清除已完成的todos
      clearCompleted(){
         this.todos = this.todos.filter(todo => !todo.done);
     },
     //修改filter的值
     setFilter(filter){
         this.filter = filter;
     },
     //编辑todo
     editTodo(todo,text){
         let index = this.todos.findIndex( tt => tt === todo);
         this.todos[index].text = text;
     }
  },
  components: {
    AddTodo,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
    @import "./assets/todo-mvc.css"
</style>
