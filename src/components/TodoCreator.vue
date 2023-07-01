
<script setup>
     import { reactive, defineEmits } from 'vue';
     import TodoButton from './TodoButton.vue'

     const emit = defineEmits(['create-todo'])

     const todoState = reactive({
        todo: "",
        invalid: null,
        errMsg: "",
     })
    


     const createTodo = () => {
        todoState.invalid = null

        if (todoState.todo !== "") {
          emit ('create-todo', todoState.todo)
          todoState.todo = ""
          return
        }  
        todoState.invalid = true
        todoState.errMsg = "Todo Input cannot be empty!"

     }
</script>

<template>
    <div 
    class="input-wrap"
    :class="{ 'input-err': todoState.invalid}"
    >
        <input type="text" v-model="todoState.todo">
         <TodoButton @click="createTodo()"/>
    </div>
   <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
</template>


<style lang="scss" scoped>
  .input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
    animation: pulse 1.5s infinite;

    @keyframes pulse {
  0% {
    border-color: rgba(255, 0, 0, 0.2);
  }
  50% {
    border-color: rgba(255, 0, 0, 1);
  }
  100% {
    border-color: rgba(255, 0, 0, 0.2);
  }
}
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  
}

.err-msg {
  margin-top: 14px;
  margin-bottom: 10px;
  font-size: 12px;
  font-weight: 600;
  text-align: center;
  color: red;
  position: relative;
  right: 100%;
  transform: translateX(100%);
  animation: slideIn 0.5s forwards;

  @keyframes slideIn {
    0% {
      right: 500%;
      transform: translateX(100%);
    }
    100% {
      right: 100%;
      transform: translateX(100%);
    }
  }
}

</style>