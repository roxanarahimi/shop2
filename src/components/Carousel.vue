<template>
  <carousel :autoplay="1" :transition="3000" :wrap-around="true">
    <slide v-for="slide in slides" :key="slide"><img :src="slide" width="100%" alt=""></slide>

    <template #addons>
<!--      <navigation />-->
<!--      <pagination />-->
    </template>
  </carousel>
</template>
<script>
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
export default {
  props:['slides'],
  components: {
    Carousel,
    Slide,
    Pagination,
    Navigation,
  },
  data()
  {
    return{
      options:
          {
            // count of items to showed per view
            itemsToShow: {
              default: 1,
              type: Number,
            },
// count of items to be scrolled
        itemsToScroll: {
          default: 1,
          type: Number,
        },
// control infinite scrolling mode
        wrapAround: {
          default: true,
          type: Boolean,
        },
// control snap position alignment
//         snapAlign: {
//           default: 'center',
//           // validator(value: string) {
//           //   // The value must match one of these strings
//           //   return ['start', 'end', 'center'].includes(value);
//           // },
//         },
// sliding transition time in ms
        transition: {
          default: 3000,
          type: Number,
        },
// an object to pass all settings
        settings: {
          default() {
            return {};
          },
          type: Object,
        },
// an object to store breakpoints
        breakpoints: {
          default: null,
          type: Object,
        },
// time to auto advance slides in ms
        autoplay: {
          default: 0,
          type: Number,
        },
// slide number number of initial slide
        modelValue: {
          default: undefined,
          type: Number,
        },
// toggle mouse dragging.
        mouseDrag: {
          default: true,
          type: Boolean,
        },
// toggle mouse dragging.
        touchDrag: {
          default: true,
          type: Boolean,
        },
          }
    }
  }
}

</script>