<template>
  <div class="app-container">
  <h1 class="app-title">Vuejs todos</h1>

  <div class="composer">
    <Composer v-model="newTodo" @onEnter="addTodo" />
    <div class="filter">
      <div class="filter__left">
        <button @click="filter_mode = 'all'" class="filter__button filter__button--active">All ({{todoAll}})</button>
        <button @click="filter_mode = 'undone'" class="filter__button">Pending ({{undonecount}})</button>
        <button @click="filter_mode = 'done'" class="filter__button">Done ({{donecount}})</button>
      </div>
      <div>
        <button @click="clear" class="filter__button filter__button--danger">Clear</button>
      </div>
    </div>
  </div>

  <div class="todos">
    <Todo v-for="todo in todosFilters" :key="todo.id" :todo="todo" @onToggle="todoStatus" />
  </div>
</div>

</template>
<script>
import {v4 as uid} from 'uuid'
import Todo from './components/Todo.vue'
import Composer from './components/Composer.vue'
export default {
  name:"TodoApp",
  mounted(){
    this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  updated(){
    localStorage.setItem('todos', JSON.stringify(this.todos));
  },
  components:{
    Todo,
    Composer,
  },
  data() {
    return {
      newTodo: '',
      todos: [],
      allCount:0,
      filter_mode:'all'
    }  
  },
  methods:{
    addTodo(){
      const todo = {
        id:uid(),
        task:this.newTodo,
        time: new Date(),
        done:false,
      };
      this.newTodo = "";
      this.todos.unshift(todo);
    },
    todoStatus(todo){
      todo.done = !todo.done;
    },
    clear(){
      this.todos = this.todos.filter((todo) => !todo.done);
    },
    
  },
  computed:{
    todosFilters(){
      if(this.filter_mode=='all') return this.todos;
      if(this.filter_mode=='undone') 
        return this.todos.filter((todo)=> !todo.done);
      if(this.filter_mode=='done') 
        return this.todos.filter((todo)=> todo.done);
    },
    todoAll(){
      return this.todos.length;
    },
    undonecount(){
      return this.todos.filter((todo)=> !todo.done).length;
    },
    donecount(){
      return this.todos.filter((todo)=> todo.done).length;
    }
  }
}
</script>
