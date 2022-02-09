<template>
    <li 
        class="list-group-item d-flex
        align-items-center border-0 mb-2
        rounded-pill shadow p-3 mb-3 bg-body"
        v-for="(item,index) in items" :key="index"
        :class="{done: item.done}"
        >   
        <input class="form-check-input me-2 rounded-circle" type="checkbox" @click="workDone(item)" />
        {{item.title}}
        <button v-if="isVisible" class="btn btn-danger btn-sm ms-auto" @click="DeleteItem(item.id)">X</button>
    </li>
</template>

<script>
import axios from 'axios'
export default {
 data(){
    return{
      url:"https://todo-backend-laravel.herokuapp.com/api",
      items:[],
      responseData:null,
      isVisible:true
    }
  },
  mounted(){
    this.getItem()
  },
  computed:{
      listItemCount(){
          var total=0;
          this.items.forEach(item =>{
              total +=item
          })
          return total
      }
  },
  methods:{
    getItem(){
      axios.get(this.url).then(response=>{
        this.items=response.data
      })
    },
    DeleteItem(id){
        axios.delete("https://todo-backend-laravel.herokuapp.com/api/" +id).then(() =>{
        this.getItem()
        })
      
    },
    workDone(item){
      item.done =!item.done
    },
    
    //showRemoveButton(index){
      //this.items[index].isVisible= !this.item[index].isVisible
   // }
  },
}
</script>

<style>
.done{
  text-decoration: line-through;
}
</style>