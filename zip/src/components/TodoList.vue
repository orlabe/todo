
<template>

    <div class="all">
        <input type="text" class="todo-input" placeholder=" What needs to be done?" v-model="newTodo" @keyup.enter="addTodo">
        <transition-group name="fade" enter-active-class="animated fadeInUp" leave-active-class="animated fadeOutDown">
        <div v-for="(todo, index) in todosFiltered" :key="todo.id" class="todo-item"> 
          <div class="todo-item-left">
            <input type="checkbox" v-model="todo.completed">
            <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label" :class="{ completed : todo.completed }">{{ todo.title}} </div>
              <input v-else class="todo-item-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)"  @keyup.enter="doneEdit(todo)"  @keyup.esc="cancelEdit(todo)" v-focus>
        </div>
        <div class="remove-item" @click="removeTodo(index)">
            &times;
        </div>
      </div>
      </transition-group>
    <div class="extra-container">
      <div><label><input type="checkbox" :checked="!anyRemaining" @change="checkAllTodos"> Check All</label></div>

      <div> {{ remaining }} items left</div>
    </div>

      <div class="extra-container">
     <div>
        <button :class="{ active: filter =='all' }" @click="filter = 'all'">All</button>
        <button :class="{ active: filter =='active' }" @click="filter = 'active'">Active</button>
        <button :class="{ active: filter =='completed' }" @click="filter = 'completed'">Completed</button>
    </div>
    <div>
      <transition name="fade">
      <button v-if="showClearCompletedButton" @click="clearCompeted">Clear Completed</button>
      </transition>
    </div>
      </div>
      
    </div>
    

 

  
 </template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      filter: 'all',
      todos: [
        {
              'id': 1,
              'title': 'Finish Vue Project',
              'completed': false,
              'editing': false,
          },
        {
              'id': 2,
              'title': 'Present Vue Project to Class',
              'completed': false,
              'editing': false,
          },

      ]
    }
  },

  computed: {
    remaining(){
      return this.todos.filter(todo => !todo.completed).length
    },
 
  anyRemaining(){
    return this.remaining  /= 0
  },
  todosFiltered() {
    if(this.filter == 'all') {
      return this.todos
    } else if (this.filter =='active') {
      return this.todos.filter(todo => !todo.completed)

    }else if (this.filter =='completed') {
       return this.todos.filter(todo => todo.completed)
    }
    return this.todos
  },
  showClearCompletedButton() {
    return this.todos.filter(todo => todo.completed).length > 0
  }
  },

  directives: {
    focus: {
    
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
      addTodo() {
        if(this.newTodo.trim().length == 0){
          return
          }

          this.todos.push({
              id: this.idForTodo,
              title: this.newTodo,
              completed: false,

          })

          this.newTodo = '' 
          this.idForTodo++
      },
      editTodo(todo) {
        this.beforeEditCache = todo.title
        todo.editing = true
      },

      doneEdit(todo) {
         if(todo.title.trim().length == 0){
          todo.title = this.beforeEditCache 
          }
        todo.editing = false
      },

      cancelEdit(todo){
        todo.title = this.beforeEditCache
        todo.edit = false
      },

      removeTodo(index) {
        this.todos.splice(index, 1)
      },
      checkAllTodos() {
        this.todos.forEach((todo) => todo.completed =event.target.checked)
      },
      clearCompeted() {
        this.todos = this.todos.filter(todo => !todo.completed)
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  @import url(https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.0.0/animate.compat.css);
.todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
}

.todo-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  animation-duration: 0.4;
}

.remove-item {
  cursor: pointer;
  margin-left: 14px;
 
}

.remove-item:hover{
  color: rgb(48, 17, 228);
}

.todo-item-left {
  display: flex;
  align-items: center;
}

.todo-item-label {
  padding: 10px;
  border: 1px solid white;
}

.todo-item-edit {
  font-size: 24px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 5px solid  rgb(255, 145, 0);
  
  font-family: 'Aveniz', Arial, Helvetica, sans-serif;
}

.completed {
  text-decoration: line-through;
  color: rgb(235, 125, 125);
}

.extra-container {
  display: flex;
  align-items: center; 
  justify-content: space-between;
  font-size: 16px;
  border-top: 4px solid rgb(250, 163, 50);
  padding-top: 14px;
  margin-bottom: 14px;
}

button {
  font-size: 14px;
  background-color: white;
  appearance: none;

}

button:hover{
  background: rgb(223, 131, 184);
}
.active {
background: rgb(250, 163, 50);

}
.fade-enter-active, .fade-leave-active {
  transition: opacity .3s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
