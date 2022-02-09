<template>
  <p></p>
    <li 
        class="list-group-item d-flex
        align-items-center border-0 mb-2
        rounded-pill shadow p-3 mb-3 bg-body"
        v-for="(item,index) in items" :key="index"
        
        >   
        <input class="form-check-input me-2 rounded-circle" type="checkbox" @click="workDone(item)" />
        <p class="mt-3" :class="{done: item.done}">{{item.title}}</p>
        <button v-if="isVisible" class="btn btn-danger btn-large ms-auto" @click="DeleteItem(item.id)">X</button>
    </li>
    <h4>Left Work:{{activeTodoCount}} </h4>
    <BaseButton>All({{allList}})</BaseButton>
    <BaseButton>Active ({{activeTodoCount}})</BaseButton>
    <BaseButton>Completed({{doneTodoCount}})</BaseButton>
</template>

<script>
import axios from 'axios'
import BaseButton from './BaseButton.vue'
export default {
  components:{
    BaseButton,
  },
 data(){
    return{
      count:0,
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
    allList(){
      return this.items.length
    },
    activeTodoItem(){
      return this.items.filter(item =>!item.done)
    },
    activeTodoCount(){
      return this.activeTodoItem.length
    },
    doneTodoItem(){
      return this.items.filter(item =>item.done)
    },doneTodoCount(){
      return this.doneTodoItem.length
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
      item.completed =true
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
p{

}
</style>

