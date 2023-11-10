<template>
   <aside class="app-filters">
    <section class="toggle-group">
      
      <button @click="setFilter(filter)" v-for="filter of filters" class="button " :class="{'button--primary':activeFilter===filter}">{{ filter }}</button>

    </section>
  </aside>
</template>


<script lang="ts">
import { PropType, defineComponent } from 'vue';
import { Filter } from '../types/Filter';
interface state{
  filters: Filter[]
}
export default defineComponent({
props:{
  activeFilter:{
    type:String as PropType<Filter>,
    required:true,
  }
},
data():state{
  return{
    filters:["All","Active","Done", ]
  }
},
methods:{
  setFilter(filter:Filter){
this.$emit('setFilter', filter)
  }
},
emits:{
  setFilter:(filter:Filter)=>filter
}


});
</script>

<style>

</style>