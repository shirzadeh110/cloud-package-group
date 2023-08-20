<template>
  <div class="home">
    <cloud-package v-for="item of totalVuePackages" :product="item" :key="item.id"/>
  </div>
</template>

<script>
import CloudPackage from '@/components/CloudPackage.vue'

export default {
  name: 'HomeView',

  data() {
   return {
    totalVuePackages: [] 
   }
 },
  components: {
    CloudPackage
  },


created() {
  const headers = { "x-api-key": "PMAK-61325d70088f41003cdecd8a-dcb8940943ee694609eb0faf438043248d" };
  fetch("https://e6f6217f-1eb5-4d47-a974-369e92dca4e0.mock.pstmn.io/getpackageinfo", { headers })
    .then(response => response.json())
    .then(res => {
       this.totalVuePackages = res.data
    });
}
}
</script>

<style scoped lang="scss">
   @import "@/styles/pages/home.sass"
</style>
