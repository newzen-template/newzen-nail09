<!-- eslint-disable vue/html-self-closing -->
<template>
  <section
    class=""
    v-if="block.status"
    :data-cms-bind="dataBinding"
    :style="{ backgroundImage: `url(${block.background_image})`, backgroundColor:block.background_color }"

  >
    <div
      style="
        box-shadow: 9px 0px 15px 0px
          rgba(188.24999999999997, 191.25, 188.24999999999997, 0.11);
      "
      class="my__container"
      
    >
      <div style="padding-bottom: 34px;padding-top:70px" class="text-center" >
        <h2
          style="padding: 15px"
          class="title fs-1 fw-bold"
          v-html="block.title"
        ></h2>
        <div
          class="desc"
          style="font-size: 18px; color: #333333"
          v-html="block.description"
        ></div>
      </div>
      <div class="row">
          <div :class="block.style === 'Full' ? '' : 'col-12 col-sm-6 col-lg-6'" class="p-2" v-for="(item,indexParent) in block.list_service" :key="item">
            <div  class="fs-5 fw-bold font-mb"  v-html="item.title"></div>
            <div class="parent">
              <div
                v-for="(itemList, index) in item.list_item"
                :key="index"
                class="service-category"
              >
                <div
                  class="accordion-btn"
                  @click="toggleCategory(indexParent, index)"
                >
                  <img
                    class="accordion-icon"
                    style="margin-right: 5px"
                    :src="
                      activeCategories['list_item'] === index
                        ? block.image_caret_down
                        : block.image_caret_right
                    "
                     :alt="block.image_alt"
  
                  />
                  {{ itemList.title }}
                </div>
              <transition name="slide">
                  <div
                  v-if="activeCategories[`${indexParent}-${index}`] === index"
                  class="accordion-content"
                    v-html="itemList.desc"
                  ></div>
              </transition>
              </div>
            </div>
        </div>
      </div>
    </div>
  </section>
</template>
<!-- </div>     
  </div> -->
<script lang="ts" setup>
import { ref } from 'vue'

const activeCategories = ref<Record<string, number | null>>({})

const toggleCategory = (parentIndex: number, childIndex: number) => {
  const key = `${parentIndex}-${childIndex}` // Tạo key duy nhất theo từng nhóm
  activeCategories.value[key] =
    activeCategories.value[key] === childIndex ? null : childIndex
}

interface Props {
  dataBinding: any
  block: any
}
const props = defineProps<Props>()
</script>

<style lang="scss" scoped>
.accordion-btn {
  display: flex;
  align-items: center; /* Căn giữa theo chiều dọc */
  background: none; // Bỏ nền
  border: none; // Bỏ viền
  font-size: 18px; // Kích thước chữ
  color: #333; // Màu chữ
  cursor: pointer; // Giữ hiệu ứng click
  display: block; // Đảm bảo căn chỉnh tốt
  padding: 10px 0; // Khoảng cách giữa các mục
  font-weight: 700;
  font-size: 16px;
  margin-left: 10px;
  justify-content: space-between; /* Tránh bị nhảy */

  width: 100%;
}

.accordion-content {
  padding-top: 10px;
  color: #333;
  font-size: 16px;
  margin-left: 10px;
}

.service-category {
  position: relative;
  padding-bottom: 5px;

  &::before {
    content: '';
    position: absolute;
    top: -1px; /* Dịch lên một chút để đảm bảo line không bị lệch */
    left: 0;
    width: 100%;
    height: 1px;
    background-color: #d5d8dc;
  }
}
.font-mb{
  color:#3C3C3C;
}
/* Đảm bảo mục cuối cùng cũng có line */
.service-category:last-child {
  border-bottom: 1px solid #d5d8dc;
}
.parent .service-category:first-child::before,
.my__container .service-category:first-child::before {
  content: none !important;
}

@media (max-width: 1024px){
  .my__container{
  padding: 0 15px 0 15px;
}
}
@media (max-width: 568px){
  .my__container{
  padding: 60px 30px 60px 30px;
}
.font-mb{
  font-size: 26px !important;
  text-align: center;
  padding-top: 30px;
  padding-bottom: 10px;
}
}

.slide-enter-active, .slide-leave-active {
  transition: max-height 0.4s ease-in-out, opacity 0.3s ease-in-out;
  overflow: hidden;
}

.slide-enter-from,
.slide-leave-to {
  max-height: 0;
  opacity: 0;
}

.slide-enter-to,
.slide-leave-from {
  max-height: 500px; /* Điều chỉnh max-height tùy nội dung */
  opacity: 1;
}
.slide-leave {
  max-height: 200px;
  opacity: 1;
}

.slide-leave-to {
  max-height: 0;
  opacity: 0;
  transition: max-height 0.4s ease-in-out, opacity 0.1s ease-in 0.3s; 
  /* Opacity giảm sau 0.3s để đảm bảo nội dung cuộn lên trước */
}
img{
  width: 16px;
  height: 16px;
}
</style>
