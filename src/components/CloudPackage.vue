<template>
    <div class="card"
    :class="selectedPackageStatus  ? 'selected' : ''">

        <div v-if="selectedPackageStatus" class="selected-tik">
                <img src="../../public/img/tik.png"/> 
        </div>
        <div class="product-img">
              <div class="persent">
                {{ product.discountPercent }}%
               </div>
            <img :src="getImage(product.id)"/>
        </div>
        <div class="procuct-name">
            <span>
                {{product.packageName}}
            </span>
        </div>
        <div class="price">
            <span class="old-amount">   
                {{ addSeparator(product.price) }}
            </span>
            <span class="amount">   
                {{ product["discount "]?addSeparator(product.price - product["discount "])  :addSeparator(product.price - product.discount) }}
            </span>
            <span class="unit">ریال/ماهانه</span>
        </div>
        <div class="properteis">
            <div class="items">
                <div>
                    <span class="val">{{ product.ramCapcity }} گیگ </span>
                    <span class="key">: RAM</span>
                    <img src="../../public/img/ram.png"/>       
                </div>
                <div>
                    <span class="val">{{ product.trafficCapacity }}</span>
                    <span class="key">: Traffic</span>
                    <img src="../../public/img/hard.png"/>
                </div>
            </div>

            <div class="items">
                <div>
                    <span class="val">{{ product.storageCapacity }} گیگ </span>
                    <span class="key">: SSD</span>
                    <img src="../../public/img/hard.png"/>
                </div>
                <div>
                    <span class="val">{{ product.cpuCapacity }} هسته </span>
                    <span class="key">: CPU</span>
                    <img src="../../public/img/cpu.png"/>  
                </div>
            </div>
        </div>

        <div class="selected">
           <span>{{ product.duration }}</span>
            <img src="../../public/img/btn_selected.png"/>
        </div>
        <btn-praimary :productId="product.id" :selectedState="selectedPackageStatus" @selected="selectedPackage"/>
    </div>
  </template>
  
  <script>

import BtnPraimary from './Buttons/BtnPraimary.vue'

  export default {
    name: 'CloudPackage',
    data() {
        return {
            packageImages: [
                {name : "Tester Pack" , id:100, icon:'ic_enterprise.png'},
                {name : "Tester Pack" , id:101, icon:'ic_professional.png'},
                {name : "Tester Pack" , id:102, icon:'ic_startUp.png'},
                {name : "Tester Pack" , id:103, icon:'ic_professional_2.png'},
                {name : "Tester Pack" , id:104, icon:'ic_starUp_2.png'}
            ],
            selectedPackageStatus:false
        }
    },
    methods:{
        selectedPackage(item){
          this.selectedPackageStatus= this.product.id == item.productId ? true :false
        },
        getImage(id) {
             let item = null
             item = this.packageImages.find((item) => item.id == id)
             return require ("../../public/img/" + item.icon)
        },
        addSeparator(nStr) {  
            nStr = nStr/10   
            nStr += '';
            var x = nStr.split('.');
            var x1 = x[0];
            var x2 = x.length > 1 ? '.' + x[1] : '';
            var rgx = /(\d+)(\d{3})/;
            while (rgx.test(x1)) {
                    x1 = x1.replace(rgx, '$1' + '.' + '$2');
            }
        return x1 + x2;
       }
    },
   
      components: {
        BtnPraimary
    },
    props: {
      product: Object
    }
  }
  </script>
  

  <style scoped lang="scss">
   @import "@/styles/components/cloud-package.sass"
  </style>