<template>
  <header class="header">
      <h1>todos</h1>
      <input class="new-todo" placeholder="What needs to be done?" @keyup.enter="addItem"
      v-model="title">
    </header>
</template>

<script>
export default {
     props:{
        addTodo:Function
     },
    data(){
        return{
            title:''
        }
    },
     methods:{
        addItem(){
            //检查输入合法性
            const title = this.title.trim()
            if(!title){
                alert('必须输入')
                return
            }
            //根据输入生成一个todo
            const todo = {
                title,
                complete: false
            }
            //添加todo
            this.addTodo(todo)
            //清除输入
            this.title = ""
        }
    }
}
</script>

<style scoped>
.todoapp h1 {
  position: absolute;
  top: -155px;
  width: 100%;
  font-size: 100px;
  font-weight: 100;
  text-align: center;
  color: rgba(175, 47, 47, 0.15);
  -webkit-text-rendering: optimizeLegibility;
  -moz-text-rendering: optimizeLegibility;
  text-rendering: optimizeLegibility;
}

.new-todo,
.edit {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  color: inherit;
  padding: 6px;
  border: 1px solid #999;
  box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.new-todo {
  padding: 16px 16px 16px 60px;
  border: none;
  background: rgba(0, 0, 0, 0.003);
  box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03);
}
</style>
