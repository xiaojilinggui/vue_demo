<template>
  <section class="main">
      <input class="toggle-all" id="toggle-all" type="checkbox" :v-model="isAllCheck">
      <label for="toggle-all" >Mark all as complete</label>
      <ul class="todo-list" >
        <TodoItem v-for="(todo,index) in todos" :key="index" :todo ="todo" :index="index" :deleteTodo="deleteTodo"></TodoItem>
      </ul>
    </section>
</template>

<script>
import TodoItem from './TodoItem.vue'
import { filter } from 'bluebird';
export default {
    props:{
        todos:Array,
        deleteTodo:Function,
        selectAllTodos:Function,
        filter
    },
    computed:{
      completeSize(){
        return this.todos.reduce((preTotal,todo)=>preTotal +(todo.complete?1:0),0)
      },
      isAllCheck:{
        get(){
          return this.completeSize === this.todos.length
        },
        
        set(value){//value checkbox最新值
          this.selectAllTodos(value)
        }
      },
      showTodo: function() {
        let filter = this.filter;
        console.log(this.todos)
        let showTodo = this.todos.filter( data => {
          if(filter === 'all'){
            return data
          }else if( filter === 'active'){
            return !data.completed
          }else if( filter === 'completed'){
            return data.completed
          }
        })
        return showTodo
      },
    },
    components:{
        TodoItem
    }
}
</script>

<style scoped>
.main {
  position: relative;
  z-index: 2;
  border-top: 1px solid #e6e6e6;
}

.toggle-all {
  width: 1px;
  height: 1px;
  border: none; /* Mobile Safari */
  opacity: 0;
  position: absolute;
  right: 100%;
  bottom: 100%;
}

.toggle-all + label {
  width: 60px;
  height: 34px;
  font-size: 0;
  position: absolute;
  top: -52px;
  left: -13px;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}

.toggle-all + label:before {
  content: '❯';
  font-size: 22px;
  color: #e6e6e6;
  padding: 10px 27px 10px 27px;
}

.toggle-all:checked + label:before {
  color: #737373;
}

.todo-list {
  margin: 0;
  padding: 0;
  list-style: none;
}


</style>
