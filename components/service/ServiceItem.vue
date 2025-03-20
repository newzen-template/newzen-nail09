<!-- eslint-disable vue/html-self-closing -->
<template>
    <section
      class="position-relative z-1000"
      v-if="block.status"
      :data-cms-bind="dataBinding"
      :style="{backgroundImage: `url(${block.background_image})`, backgroundColor:block.background_color}"
    >
       
<div class="total my__container" >
      <div class="head" itemscope itemtype="http://schema.org/Service" >
        <meta itemprop="serviceType" :content="businessType" />
        <h2 itemprop="name" style="padding-bottom:20px"  class="heading fs-1 fw-bold fontMontserrat fs-mb " v-html="block.title"></h2>
                 <div itemprop="description" style="margin-bottom:14px" class="desc" v-html="block.desc"></div>
                     <div class="d-inline"  style="padding-bottom:14px;padding-left:5px;">
                     <NuxtLink  class="desc" style="color:#FCC5C0;font-size:18px" :to="block.link">{{ block.desc_link }}</NuxtLink>
       </div>
      </div>
      <table class="table"> 
        <thead>
          <tr >
            <th class="fontMontserrat f-5 fw-semibold thead" v-html="block.service"></th>
            <th class="fontMontserrat f-5 fw-semibold thead" style="color:#fff;background:#FCC5C0" v-html="block.regular"></th>
            <th class="fontMontserrat f-5 fw-semibold thead" v-html="block.member"></th>
          </tr>
        </thead>
        <tbody class="tbody">
          <tr v-for="(item, index) in block.list_item" :key="index" :style="{ backgroundColor: index % 2 !== 0 ? 'hsla(0, 0%, 50.2%, .1019607843)' : '' }">
            <td style="font-size:14px" class="fontMontserrat" v-html="item.title"></td>
            <td style="font-size:14px" class="fontMontserrat" v-html="item.price"></td>
            <td style="font-size:14px" class="fontMontserrat" v-html="item.member"></td>
          </tr>
        </tbody>
      </table>
</div>


   
    </section>
  </template>
  <!-- </div>     
  </div> -->
  <script lang="ts" setup>
import SITE from '@/data/site.json';

const dataSite: any = ref(SITE);
const firstKey = Object.keys(SITE)[0];
const lengthType = dataSite.value[firstKey].business_type.split('/').length;
const businessType = dataSite.value[firstKey].business_type.split('/')[lengthType - 1];

  interface Props {
    dataBinding: any;
    block: any;
  }
  const props = defineProps<Props>();
  console.log(props)
  </script>
  
<style lang="scss" scoped>
.custom-color{
  color:#FCC5C0 !important;
  background-color: red;
}
.table{
  margin-bottom: 0 !important;
}
.head{
  text-align: center;
  box-shadow: 0px 0px 15px 0px rgba(188.24999999999997, 188.24999999999997, 188.24999999999997, 0.11);
    transition: background 0.3s, border 0.3s, border-radius 0.3s, box-shadow 0.3s;
    margin: 0px 0px 0px 0px;
    --e-column-margin-right: 0px;
    --e-column-margin-left: 0px;
    padding: 70px 0px 0px 0px;
}  

td{
  border-style: none;
}
.desc{
  color:#333333;
  font-size: 18px;
   & :deep(a)   {
    color:#FCC5C0;
  }
}

.thead{
  background-color:#FCC5C0 !important;
  color:#fff;
}
th,td{
  padding: 20px 15px;
  background-color: transparent !important;
}
.tbody {
  &tr {
    &td{
      background-color: transparent !important;
    }
  }
}
tr:nth-child(odd){
  background-color: hsla(0, 0%, 50.2%, .0705882353) !important;
}
 tr:nth-child(odd):hover {
    background-color: hsla(0, 0%, 50.2%, .1019607843) !important;
}
tr:nth-child(odd):hover{
  background-color: red;
}

@media (max-width: 1024px){
  .my__container{
    padding-left: 15px;
    padding-right: 15px;
  }
}

@media (max-width: 768px){
  .my__container{
    padding-left: 15px;
    padding-right: 15px;
  }
}

@media (max-width: 568px){
  .fs-mb{
    font-size: 26px !important;
  }
  .my__container{
    padding-left: 30px;
    padding-right: 30px;
  }
 
  .desc{
    font-size: 16px !important;
  }
}
</style>
  