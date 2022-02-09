<template>
<div class="d-flex justify-content-center">
    <button type="button" class="btn btn-success rounded-circle" data-bs-toggle="modal" data-bs-target="#exampleModal">
        +
    </button>
</div>
<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Add Your List</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
          <form @submit.prevent="UserItem">
              <input type="text" class="form-control" v-model="singleItem.title">
              <button type="submit" class="btn btn-success mt-2">Submit</button>
          </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-success" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            url:"https://todo-backend-laravel.herokuapp.com/api",
            singleItem:{
                title:""
            },
            responseData: null,
        }
    },
    methods:{
        UserItem(){
        axios.post(this.url,this.singleItem).then(response=>{
            this.responseData=response.data
            this.singleItem.title=""
            alert("Item Added")
        })
    }
   }

}
</script>

<style>

</style>