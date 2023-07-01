<script setup>
 import { ref, watch, computed } from 'vue';
 import TodoCreator from '../components/TodoCreator.vue';
 import TodoItem from '../components/TodoItem.vue';
 import { uid } from 'uid'
 import { Icon } from '@iconify/vue';

 const todoList = ref([])
 
 watch(
  todoList, 
   () => {
    setTodoListLocalStorage()
  }, 
  {
   deep: true,
   }
 )

 const todoCompleted = computed(() => {
    return todoList.value.every((todo) => todo.isCompleted)
 })


 const fetchTodoList = () => {
   const savedTodoList = JSON.parse(localStorage.getItem('todoList'))
   if (savedTodoList) {
     todoList.value = savedTodoList
   }
 }
 fetchTodoList()

 const setTodoListLocalStorage = () => {
    localStorage.setItem('todoList', JSON.stringify(todoList.value))
 }


 const createTodo = (todo) => {
    todoList.value.push({
      id: uid(),
      todo,
      isCompleted: null,
      isEditing: null
    })
   
 }

 const toggleTodoComplete = (todoPosition) => {
    todoList.value[todoPosition].isCompleted = !todoList.value[todoPosition].isCompleted
     
 }

 const toggleEditTodo = (todoPosition) => {
  todoList.value[todoPosition].isEditing = !todoList.value[todoPosition].isEditing 
  
 }

 const updateTodo = (todoValue, todoPosition) => {
   todoList.value[todoPosition].todo = todoValue
   
 }

 const deleteTodo = (todoId) => {
    todoList.value = todoList.value.filter((todo) => todo.id !== todoId)
    
 }

</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul todo-list v-if="todoList.length > 0">
      <TodoItem 
      v-for="(todo, index) in todoList"
      :todo="todo"
      :index="index"
      @toggle-complete="toggleTodoComplete"
      @edit-todo="toggleEditTodo"
      @update-todo="updateTodo"
      @delete-todo="deleteTodo"
      />
    </ul>
    <p class="todos-msg" v-else>
      <Icon 
      icon="noto-v1:sad-but-relieved-face"  
      width="22" 
      height="22" 
      />
      <span>
        You have no todos to complete at the moment! Add one!
      </span>
    </p>
    <p 
    v-if="todoCompleted && todoList.length > 0"
    class="todos-msg"
    >
    <Icon icon="noto-v1:party-popper" />
    <span>You have completed all your todos!...Hurray!</span>
    <Icon icon="noto-v1:party-popper" />
  </p>
  </main>
</template>

<style lang="scss" scoped>
  main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
    font-size: 14px;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
    position: relative;
    left: 100%;
    transform: translateX(100%);
    animation: slideIn 0.5s forwards;

  @keyframes slideIn {
    0% {
      left: 500%;
      transform: translateX(100%);
    }
    100% {
      left: -100%;
      transform: translateX(100%);
    }
  }
    
    span {
      font-size: 11px;
      font-weight: 400;
      color: rgb(126, 122, 118);
    }
  }
}
</style>
