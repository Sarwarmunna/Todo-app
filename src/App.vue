<template>
  <!-- <div>
    <h1>Welcome to vue js via vite js</h1>
    <a :href="link">google</a>
    <h2>Count:{{count}}</h2>
    
    <button @click="count++">+</button>
    <button @click="count--">-</button>
    <h2>Name:{{person.name}}</h2>
    <div class="box" :style="{
      backgroundColor: color,
      width: width + 'px',
      height: height + 'px',
      }">   
    </div>
    <person :name="person.name" :age="person.age">
      <p>Lorem ipsum dolor sit amet, 
        consectetur adipisicing elit. Corporis, 
        ducimus modi voluptas placeat commodi quod 
        deleniti temporibus pariatur nihil itaque nam 
        magnam quae explicabo ad iure ut praesentium tenetur adipisci?</p>
      </person>
    <input type="text" v-model="person.name"> <br> <br>
    <input type="text" v-model="person.age"> <br> <br>
    
          <input type="color" v-model="color">
          <input type="range" v-model="width">
          <input type="range" v-model="height">
  </div> -->
<layout>
  <h1 class="app-title">Vuejs todos</h1>

  <div class="composer">
  <composer 
  v-model="newTodo" 
  @onEnter="addTodo"
   />
    <div class="filter">
      <div class="filter__left">
        <button @click="filter_mode='all'" class="filter__button filter__button--active">All ({{totalcount}})</button>
        <button @click="filter_mode='undone'" class="filter__button">Pending ({{undonecount}})</button>
        <button @click="filter_mode='done'" class="filter__button">Done ({{donecount}})</button>
      </div>
      <div>
        <button class="filter__button filter__button--danger" @click="clear">Clear</button>
      </div>
    </div>
  </div>

  <div class="todos">
   

    <!-- Todo start -->
    <todo  v-for="todo in filterTodos" 
    :key="todo.id" 
    :todo="todo" 
    @ontoggle="addtoggle"
    />
    <!-- Todo end -->
  </div>

</layout>
</template>


<script>
import todo from "./components/todo.vue";
import composer from "./components/composer.vue";
import layout from "./components/layout.vue";
export default {
  name:"todoapp",
  components:{
    todo,
    composer,
    layout
  },
  data() {
    return {
      newTodo:"",
      todos:[],
      filter_mode:"all",
    };
  },
  methods: {
    
    addTodo(e) {
      const todo = {
        id: Date.now(),
         task: this.newTodo,
         time:"Monday",
         done: false,
      };
      this.todos.unshift(todo);
      this.newTodo="";

    },
    addtoggle(todo){
      todo.done = !todo.done;
    },
    clear() {
      this.todos = this.todos.filter((todo) => !todo.done);
    } 
  },
  computed:{
    filterTodos(){
     if(this.filter_mode == "all")return this.todos;
     if(this.filter_mode == "done")
     return this.todos.filter((todo) => todo.done);
     if(this.filter_mode == "undone")
     return this.todos.filter((todo) => !todo.done);
    },
    totalcount(){
    return this.todos.length;
    },
    donecount(){
      return this.todos.filter((todo) => todo.done).length;
    },
    undonecount(){
      return this.todos.filter((todo) => !todo.done).length;
    }
  }
}
</script>