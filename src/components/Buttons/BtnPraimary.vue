<template>
    <button class="btn-primary" @click="selectedPackage()">
         انتخاب
         <div :class="selectedState ? 'notActive' : 'active'">
             <img v-if=!selectedState  src="../../../public/img/tik.png"/> 
             <img v-if=selectedState src="../../../public/img/tik-active.png"/> 
         </div>
    </button>
  </template>
  
  <script>
  export default {
    name: 'BtnPraimary',
  methods: {
    selectedPackage () {
      this.$emit('selected',{ productId: this.productId});
    },
  },
    props: {
    selected: {
      type: Function
    },
    selectedState:{
      type:Boolean,
      default:false
    },
      productId: Number
    }
  }
  </script>
  
 
  <style scoped lang="scss">
    @import "@/styles/components/buttons.sass"
  </style>
  