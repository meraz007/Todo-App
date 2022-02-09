<template>
  <div class="home">
  <section class="vh-100 gradient-custom">
  <div class="container py-5 h-100">
    <div class="row d-flex justify-content-center align-items-center h-100">
      <div class="col col-xl-10">
        <div class="card">
          <div class="card-body p-5">
            <Header />
            <BaseButton>All</BaseButton>
            <BaseButton>Active</BaseButton>
            <BaseButton>Completed</BaseButton>
            <ul>
              <BaseListItem />
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
import BaseListItem from '../components/BaseListItem.vue'
import Header from '../components/Header.vue'
import InputItem from '../components/InputItem.vue'
import BaseButton from '../components/BaseButton.vue'
export default {
  components:{
    Header,
    InputItem,
    BaseButton,
    BaseListItem
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

</style>
