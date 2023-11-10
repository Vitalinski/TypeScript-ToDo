<template>
   <li @click="toggleToDo" class="todo-item" :class="{'todo-item--done': toDo.completed}">
        <div class="todo-item__status">
          <i class="bi bi-check2"></i>
        </div>
        <span class="todo-item__text">{{ toDo.text }}</span>
        <button @click.stop="removeToDo" class="todo-item__remove-button">
          <i class="bi bi-trash3"></i>
        </button>
      </li>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue';
import {ToDo} from '/home/vitalik/Рабочий стол/Frontend/TypeScript/TypeScript ToDo/src/types/ToDo.ts'

export default defineComponent( {
props:{
    toDo:{
        type:Object as PropType<ToDo>,
        required:true,
    }
},
methods:{
  toggleToDo(){
    this.$emit('toggleToDo', this.toDo.id)
  },
  removeToDo(){
    this.$emit('removeToDo', this.toDo.id)
  }
},
emits:{
  removeToDo:(id:number)=> Number.isInteger(id),

  toggleToDo:(id:number)=> Number.isInteger(id),
}
})
</script>

<style>

</style>