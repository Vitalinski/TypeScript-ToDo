
<template>
  <AppHeaderVue> </AppHeaderVue>

  <AppFilters :active-filter="activeFilter" @set-filter="setFilter"> </AppFilters>

  <AppList :toDos="filredToDos" 
  @remove-to-do="removeToDo"
  @toggle-to-do="toggleToDo"> </AppList>

  <AppAdd @add-to-do="addToDo" ></AppAdd>
  <AppFooter :stats="stats"></AppFooter>
</template>

<script  lang="ts">
import { defineComponent } from "vue";
import AppAdd from "./components/AppAdd.vue";
import AppFilters from "./components/AppFilters.vue";
import AppFooter, {stats} from "./components/AppFooter.vue";
import AppHeaderVue from "./components/AppHeader.vue";
import AppList from "./components/AppList.vue";
import { ToDo } from "./types/ToDo";
import { Filter } from "./types/Filter";



interface state {
  toDos: ToDo[];
  activeFilter: Filter
}
export default defineComponent({
  components: {
    AppHeaderVue,
    AppFilters,
    AppList,
    AppAdd,
    AppFooter,

  },
  
  data(): state {
    return {
      toDos: [
        {
          id: 0,
          text: "Learn the basics of Vue",
          completed: true,
        },
        {
          id: 1,
          text: "Learn the basics of Typescript",
          completed: false,
        },
        {
          id: 2,
          text: "Subscribe to the channel",
          completed: false,
        },
      ],
      activeFilter: 'All'
    };
  },
computed:{
filredToDos(): ToDo[]{
switch(this.activeFilter){
  case'All':
  return this.toDos
  case'Active':
  return this.activeToDos
  case'Done':
  return this.doneToDos
}
},
stats():stats {
  return{
    active: this.activeToDos.length,
    done: this.doneToDos.length

  }
},
activeToDos():ToDo[]{
  return this.toDos.filter(ToDo => !ToDo.completed)
},
doneToDos():ToDo[]{
  return this.toDos.filter(ToDo => ToDo.completed)
}
},
  methods:{
    addToDo(task:ToDo){
      this.toDos.push(task)
    },
    toggleToDo(id:number){
const targetToDo = this.toDos.find(item => item.id === id)
if(targetToDo){
    targetToDo.completed = !targetToDo.completed
}
    },
    removeToDo(id:number){
    this.toDos = this.toDos.filter(item => item.id !== id)
 
    },

    setFilter(filter:Filter){
      this.activeFilter = filter
    }
  }
});
</script>


