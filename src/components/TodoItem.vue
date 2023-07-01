<script setup>

import { Icon } from '@iconify/vue';

 const props = defineProps({
    todo: {
        type: Object,
        required: true,
    },

    index: {
        type: Number,
        required: true,
    }
 })

 defineEmits(['toggle-complete', 'edit-todo', 'update-todo', 'delete-todo'])

</script>

<template>
   <li>

    <input 
    type="checkbox" 
    :checked="todo.isCompleted"
    @input="$emit('toggle-complete', index)"
    />

    <div class="todo">
        <input 
        v-if="todo.isEditing"
        type="text" 
        :value="todo.todo"
        @input="$emit('update-todo', $event.target.value, index)"
        />
        <span 
        v-else
        :class="{'completed-todo' : todo.isCompleted}"
        >
            {{ todo.todo }}
        </span>
    </div>

    <div class="todo-actions">
        <Icon 
        v-if="todo.isEditing"
         icon="material-symbols:check-circle-outline" 
          color="#41b080"
         width="22"
          height="22" 
           class="icon"
           @click="$emit('edit-todo', index)"
          />

          <Icon 
          v-else
          icon="fa6-solid:pencil" 
          color="purple" 
          width="12" 
          height="12" 
          class="icon"
          @click="$emit('edit-todo', index)"
          />

          <Icon 
          icon="bi:trash" 
          color="#f95e5e" 
          width="16" 
          height="16" 
           class="icon"
           @click="$emit('delete-todo', todo.id)"
          />
 
    </div>

   </li>
</template>



<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    cursor: pointer;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);

    &:checked {
      background-color: #41b080;
    }
  }

  .todo {
    flex: 1;

    .completed-todo {
        text-decoration: line-through;
    }

    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #41b080;
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;
    align-items: center;
    justify-content: center;
    .icon {
      cursor: pointer;
      width: 18px;
      margin-bottom: 8px;
    }
  }
}
</style>