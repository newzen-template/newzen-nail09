<template>
  <section
    v-if="block.status"
    :data-cms-bind="dataBinding"
    :style="{ backgroundImage: `url(${block.image_background})`,backgroundColor: block.background_color }"
    style="background-position: center;margin-bottom:96px"
    class="wh count-section"
    
  >
    <div style="width: 100%; height: 100%" class="">
      <div class="backgroundOverlay"></div>
      <div class="w-bg">
        <div class="cus-bg">
          <div class="cus-img my__container">
            <div
              class="d-flex cus-row row justify-content-between text-center mt"
            >
              <div
                v-for="(item, index) in block.list_item"
                :key="index"
                class="col-6 col-sm-3 col-lg-3 col-3"
              >
                <div ref="counters" :style="{color: block.color}" class="fs-69 counter" :data-target="item.count_up"></div>
                <div class="fs-5 desc-mb" v-html=" item.title"></div>
              </div>

              <!-- <div class="col-6 col-sm-3 col-lg-3 col-3">
                <span class="fs-69" ref="trainningCounter">0</span>
                <div  class="fs-5 desc-mb" v-html="block.list_stats.stats_trainning"></div>
              </div>
        
              <div class="col-6 col-sm-3 col-lg-3 col-3">
                <span class="fs-69" ref="treatmentCounter">0</span>
                <div class="fs-5 desc-mb" v-html="block.list_stats.stats_treatment"></div>
              </div>
        
              <div class="col-6 col-sm-3 col-lg-3 col-3">
                <span  class="fs-69" ref="productCounter">0</span>
                <div class="fs-5 desc-mb" v-html="block.list_stats.stats_procuduct"></div>
              </div>    -->
            </div>
          </div>
        </div>
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
// const userCounter = ref<HTMLElement | null>(null);
// const trainningCounter = ref<HTMLElement | null>(null);
// const treatmentCounter = ref<HTMLElement | null>(null);
// const productCounter = ref<HTMLElement | null>(null);

// const animateCounter = (element: HTMLElement | null, target: number, duration: number,isUserCounter: boolean = false) => {
//   if (!element) return;

//   let current = 0;
//   const step = (target / (duration / 20));
//   const timer = window.setInterval(() => {
//     current += step;
//     element.innerText = Math.floor(current).toLocaleString();
//     if (current >= target) {
//       element.innerText = isUserCounter
//         ? target.toLocaleString() + "+"  // Thêm dấu "+" chỉ cho userCounter
//         : target.toLocaleString();
//       clearInterval(timer);
//     }
//   }, 20);
// };

// onMounted(() => {
//   const observer = new IntersectionObserver((entries) => {
//     entries.forEach((entry) => {
//       if (entry.isIntersecting) {
//         animateCounter(userCounter.value,props.block.list_count_stats.stats_user, 2000,true);
//         animateCounter(trainningCounter.value, props.block.list_count_stats.stats_trainning, 2000);
//         animateCounter(treatmentCounter.value, props.block.list_count_stats.stats_treatment, 2000);
//         animateCounter(productCounter.value, props.block.list_count_stats.stats_product, 2000);
//         observer.disconnect(); // Chạy 1 lần
//       }
//     });
//   }, { threshold: 0.5 });

//   observer.observe(userCounter.value!);
// });

const counters = ref();

onMounted(() => {
 ///counter:any
  const animateCounter = (counter:any) => {
    const target = +counter.getAttribute('data-target');
    let current = 0;
    const increment = target / 100; // Điều chỉnh tốc độ đếm

    const updateCounter = () => {
      current += increment;
      counter.innerText = Math.ceil(current).toLocaleString();

      if (current < target) {
        requestAnimationFrame(updateCounter);
      } else {
        counter.innerText = target.toLocaleString(); // Đảm bảo đạt đến giá trị đích
      }
    };
    updateCounter();
  };

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          animateCounter(entry.target);
          observer.unobserve(entry.target); // Chỉ đếm một lần
        }
      });
    },
    { threshold: 0.1 } // Kích hoạt khi phần tử hiển thị ít nhất 10%
  );

  counters.value.forEach((counter:any) => {
    observer.observe(counter);
  });
});


</script>

<style lang="scss" scoped>
.cus-bg {
  background-position: center center;
  width: 100%;
  height: 172%;
}

.wh {
  transition: background 0.3s, border 0.3s, border-radius 0.3s, box-shadow 0.3s;
  padding: 10em 0em 10em 0em;
  background-image: url("image.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-color: rgba(255, 200, 200, 0.3); /* Màu phủ */
  background-blend-mode: overlay; /* Pha trộn màu và ảnh */
}

.fs-69 {
  font-size: 69px;
  font-weight: 600;
}
@media (max-width: 1024px) {
  .wh {
    margin-bottom: 0;
  }
  .cus-row {
    margin: 10px;
  }
}

@media (max-width: 768px) {
  .wh {
    margin-bottom: 0;
  }
  .cus-row {
    margin: 10px;
  }
}
@media (max-width: 576px) {
  .fs-69 {
    font-size: 55px;
  }
  .desc-mb {
    font-size: 16px;
  }
  .wh {
    padding: 0 !important;
    padding-top: 57px !important;
    padding-bottom: 57px !important;
    background-position: center;
  }
  .cus-row {
    margin: 10px;
  }
}
</style>
