<template>
  <section 
      v-if="block.status" 
      :style="{background:block.background_color}" 
      :data-cms-bind="dataBinding" 
      class="custom-mt"
  >
    <div class="my__container row d-flex" itemscope itemtype="http://schema.org/AboutPage">
       <div class=" col-12 col-sm-6 col-lg-6 col-6 text-end position-relative pd">
         <img style="max-height: 619px;"  v-if="block.list_img.image_big" itemprop="image" class="me-3 w-ip" :src="block.list_img.image_big" />
         <img  v-if="block.list_img.image_large" class="position-absolute z-2 img-mb" style="left: -8%;top:-20%;max-height:153px":src="block.list_img.image_large" :alt="block.image_large_alt">
         <img  class="position-absolute" style="left: 26%;top:-20%;max-height: 197px;"  src="/images/hero-leafs.png" :alt="block.list_img.image_large_alt">
         <img   class="position-absolute"  style="right:8%;top:-25%;max-height: 99px;"  src="/images/hero-dots-1.png" :alt="block.list_img.image_large_alt">
         <img   class="position-absolute" style="left:3%;bottom:-8%;max-height: 99px;" src="/images/hero-dots-2.png" :alt="block.list_img.image_large_alt">
 
       </div>
       <div class=" col-12 col-sm-6 col-lg-6 col-6 d-flex flex-column align-items-start gap-4 justify-content-center" style="padding:10px">
          <div class="fs-5 fontMontserrat fw-normal fs-mb" style="text-transform: uppercase;" v-html="block.session" :style="{color: block.color}"></div>
          <div itemprop="name" class="fs-1 fontMontserrat fw-bold colortx1 title-mb" v-html="block.title"></div>
          <div itemprop="description" class="desc-mb" v-html="block.desc"></div>
            
            <NuxtLink :style="{backgroundColor: block.button.background_color, color: block.button.color}" :to="block.button.link" itemprop="url" v-if="block.button.is_show" class="btn-book d-inline-flex fz18 text-decoration-underline text-mb"  style="padding:15px 40px">{{block.button.text  }}  </NuxtLink>
       </div>
    </div>
  </section>
</template>
<script lang="ts" setup>
interface Props {
  dataBinding: any;
  block: any;
}

const props = defineProps<Props>();
</script>

<style lang="scss" scoped>
.pd{
  padding: 10px;
}
.custom-mt{
  margin-top: 6em;
  margin-bottom: 6em;
    padding: 5em 0em 3em 0em;
}

.fs-1{
  font-size: 40px !important;
}
@media (max-width: 1024px){
  .w-ip{
    width: 407px;
  }
  .custom-mt{
    margin-top: 0;
  }
  .desc-mb{
    width: 444px;
  }
}

@media  (max-width: 768px){
  .w-ip{
    width: 303px;
  }
  .custom-mt{
    margin-top: 3em;
  }
  .fs-1{
    min-width: 330px;
  }
  .title-mb{
    width: 333px;
  }
  .desc-mb{
    width: 333px;
  }
}

@media (max-width: 576px){
  .w-ip{
    width: 315px !important;
  }
  .img-mb{
    width: 160px;
  }
  .fs-mb{
    margin-top: 30px;
  }
  .title-mb{
    font-size: 26px !important;
  }
  .desc-mb{
    width: 394px;
    margin-bottom: 16px !important;
  }
  .text-mb{
    font-size: 16px;
  }
  .custom-mt{
    padding-bottom: 0 !important;
  }
}

</style>