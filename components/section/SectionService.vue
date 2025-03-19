<!-- eslint-disable vue/html-self-closing -->
<template>
  <section class="bg-img " v-if="block.status" :data-cms-bind="dataBinding" :style="{backgroundColor: block.background_color}">
    <div class="section_hero container-xl" style="padding: 80px 0 0px 0">
      <div class="text-center mb">
        <div
          class="heading fs-5 fontMontserrat fw-regular mb-4"
          :style="{ color: block.color }"
          style="text-transform:uppercase"
          v-html="block.heading"
        ></div>
        <h2
          class="title fs-1 fontMontserrat fw-bold title-mb"
          v-html="block.title"
        ></h2>

        <div class="position-relative">
          <img
            itemprop="image"
            style="right: 0; margin-top: -2%; z-index: -1"
            class="position-absolute dot-ip"
            :src="block.image"
          />
        </div>
      </div>

      <div class="row my__container cus-size">
        <div
          class="col-12 col-sm-4 col-lg-4 col-4"
          v-for="(item, index) in block.list_service"
          :key="index"
          itemscope itemtype="http://schema.org/Service"
        >
          <meta itemprop="serviceType" :content="businessType" />
          <div
            class="service_item"
            :class="{ item: index === 1 || hoverIndex === index }"
            @mouseover="hoverIndex = index"
            @mouseleave="hoverIndex = -1"
          >
            <div class="d-flex flex-column mb-3 pd">
              <div
                class="text-center d-flex flex-column justify-content-center align-items-center pt-3"
              >
                <img itemprop="image" class="img-cus" :src="item.img" :alt="block.image_alt" />
                <h3 itemprop="name" class="fs-4 p-3">{{ item.title }}</h3>
                <div itemprop="description" class="p-2" v-html="item.desc"></div>
                <NuxtLink itemprop="url" class="btn-book fontMontserrat"
                  ><span
                    class="cus-btn text-decoration-underline fw-medium"
                    style="padding: 11px 30px"
                    >{{ block.button.text }}</span
                  ></NuxtLink
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

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
import { ref } from "vue";

const hoverIndex = ref(-1);
</script>

<style scoped>
.service-item {
  transition: background 0.3s, border 0.3s, border-radius 0.3s, box-shadow 0.3s;
  background-color: #fff;
}
.item {
  outline: 4px solid #fcc5c0;
  border-radius: 30px 30px 30px 30px;
}
.mb {
  margin-bottom: 40px;
}
.cus-size {
  overflow: hidden;
  margin-top: -3em;
  margin-bottom: 0em;
  padding: 4em 0em 0em 0em;
}
.pd {
  padding: 40px 20px 40px 20px;
  border-style: solid;
  background-color: #fff;
}
.img-cus {
  height: 120px;
  object-fit: contain;
}
@media (max-width: 1024px) {
  .section_hero {
    padding-top: 0 !important;
    padding-bottom: 0 !important;
  }
  .py-5 {
    padding-bottom: 0 !important;
  }
  .dot-ip {
    margin-top: -30px !important;
  }
  .heading{
    margin-top: 80px;
  }
}
@media (max-width: 768px) {
  .section_hero {
    padding-top: 0 !important;
    padding-bottom: 0 !important;
  }
  .heading{
    margin-top: 80px;
  }
}
@media (max-width: 576px) {
  .title-mb {
    /* font-size: 26px !important; */
  }
    .heading{
      margin-top: 80px;
    }
  .dot-ip{
    display: none;
  }
}
</style>
