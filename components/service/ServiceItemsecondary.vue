<template>
  <!-- <section
    v-if="block.status"
    :style="{ background: block.background_color }"
    :data-cms-bind="dataBinding"
    class="py-4"
  >
    <div  style="
        box-shadow: 9px 0px 15px 0px
          rgba(188.24999999999997, 191.25, 188.24999999999997, 0.11)" class="my__container  ">
      <div style="padding-bottom: 34px" class="text-center">
        <div class="d-flex justify-content-start item-center">
          <img
            class="accordion-icon"
            style="margin-right: 5px"
            :src="block.image_caret_down"
            :alt="block.image_alt"
          />
          <h2 class="title">{{ block.title }}</h2>
        </div>
        <div
          class="desc"
          style="font-size: 18px; color: #333333"
          v-html="block.desc"
        ></div>
        <div v-if="block.list_item?.length > 0" class="">
          <div
            class="text-start"
            v-for="(item, index) in block.list_item"
            :key="index"
          >
            <h3 class="title">{{ item.title }}</h3>
            <div class="" v-html="item.desc"></div>
          </div>
        </div>
      </div>
      <div v-if="block.second_cat?.length > 0" class="row">
        <div
          v-for="(itemSecond, indexSecond) in block.second_cat"
          :key="indexSecond"
          style="padding-bottom: 34px"
          class="text-center col-6"
        >
          <h2 style="padding: 15px" class="title">{{ itemSecond.title }}</h2>
          <div
            class="desc"
            style="font-size: 18px; color: #333333"
            v-html="itemSecond.desc"
          ></div>
          <div v-if="itemSecond.list_item?.length > 0" class="">
            <div
              class="text-start"
              v-for="(item, index) in itemSecond.list_item"
            >
              <h3 class="title">{{ item.title }}</h3>
              <div class="" v-html="item.desc"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section> -->
</template>

<script lang="ts" setup>
interface Props {
  dataBinding: any;
  block: any;
}
const props = defineProps<Props>();
</script>

<style lang="scss" scoped>
.title {
  font-size: 16px;
  font-weight: 700;
}
.accordion-icon {
  max-width: 10px;
  max-height: 10px;
}
</style>
