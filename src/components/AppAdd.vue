<template>
   <section class="add-todo">
    
      <form @submit.prevent="addToDo" v-if="isFormVisible" class="add-todo__form">
        <button @click="isFormVisible=false" class="close-button" type="button">
          <i class="bi bi-x"></i>
        </button>
        <div class="text-input text-input--focus">
          <input v-model="text" class="input" />
        </div>
        <button  class="button button--filled">Add task</button>
      </form>
      <button v-else 
      @click="isFormVisible=true" class="add-todo__show-form-button">
        <i class="bi bi-plus-lg"></i>
      </button>
    </section>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ToDo } from '../types/ToDo';
interface state{
  isFormVisible:boolean,
  text:string
}


export default defineComponent ({


  data():state{
    return{
      isFormVisible: false,
      text:''
    }
  },
  methods:{
     addToDo(){
      this.$emit('addToDo', {
        id: Date.now(),
        text: this.text,
        completed: false
      })
      this.text=''
this.isFormVisible=false
    }
  },
  emits:{
    addToDo:(task: ToDo)=> task
  }
})
</script>

<style>

</style>