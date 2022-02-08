<template>
  <div class="home">
  <section class="vh-100 gradient-custom">
  <div class="container py-5 h-100">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col col-xl-10">
        <div class="card">
          <div class="card-body p-5">
            <Header />
            <p class="text-muted pb-2"></p>
            <ul>
              <li 
              class="list-group-item d-flex
               align-items-center border-0 mb-2
              rounded-pill shadow p-3 mb-3 bg-body"
              v-for="(item,index) in items" :key="index"
              :class="{done: item.done}"
              @mouseover="showItem(index)"
              >
                <input class="form-check-input me-2 rounded-circle" type="checkbox" @click="workDone(item)" />
                {{item.title}}
                <button v-if="isVisible" class="btn btn-danger btn-sm ms-auto" @click="DeleteItem(index)">
                  X
                </button>
              </li>
            </ul>
            <InputItem/>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
  </div>
</template>

<script>
import axios from 'axios'
import Header from '../components/Header.vue'
import InputItem from '../components/InputItem.vue'
export default {
  components:{
    Header,
    InputItem
  },
  data(){
    return{
      url:"https://todo-backend-laravel.herokuapp.com/api",
      items:[],
      responseData:null,
      isVisible:false
    }
  },
  mounted(){
    this.getItem()
  },
  methods:{
    getItem(){
      axios.get(this.url).then(response=>{
        this.items=response.data
      })
    },
    DeleteItem(index){
      this.items.splice(index,1)
    },
    workDone(item){
      item.done =!item.done
    },
    showItem(index){
      this.items[index].isVisible= !this.items[index].isVisible
    }
  },
}
</script>

<style>
  .gradient-custom {
  background: radial-gradient(50% 123.47% at 50% 50%, #00ff94 0%, #720059 100%),
    linear-gradient(121.28deg, #669600 0%, #ff0000 100%),
    linear-gradient(360deg, #0029ff 0%, #8fff00 100%),
    radial-gradient(100% 164.72% at 100% 100%, #6100ff 0%, #00ff57 100%),
    radial-gradient(100% 148.07% at 0% 0%, #fff500 0%, #51d500 100%);
  background-blend-mode: screen, color-dodge, overlay, difference, normal;
}
.done{
  text-decoration: line-through;
}
</style>
