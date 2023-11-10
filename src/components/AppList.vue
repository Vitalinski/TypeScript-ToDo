<template>
  <ul class="todo-list">
    <AppToDoItem
    @toggleToDo="toggleToDo"
    @removeToDo="removeToDo"
      v-for="toDo of toDos"
      :key="toDo.id"
      :toDo="toDo"
    ></AppToDoItem>
  </ul>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import AppToDoItem from "./AppToDoItem.vue";
import { ToDo } from "../types/ToDo";

export default defineComponent({
  components: {
    AppToDoItem,
  },
props:{
    toDos:{
        type:Array as PropType <ToDo[]>
    }
},
methods:{

    toggleToDo(id:number){
this.$emit('toggleToDo', id)
    },
    removeToDo(id:number){
        this.$emit('removeToDo', id)

    }
  },
 emits:{
    removeToDo:(id:number)=> Number.isInteger(id),

toggleToDo:(id:number)=> Number.isInteger(id),
 }

});
</script>

<style></style>
