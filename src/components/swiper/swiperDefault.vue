<template>
    <div>
        <swiper :options="swiperOption">
            <swiper-slide class="swiper-slide" v-for="(item, index) in slide" :key="index">
                Slide {{item}}
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
    </div>
</template>

<script>
import "swiper/dist/css/swiper.css";
import { swiper, swiperSlide } from "vue-awesome-swiper";
export default {
    data() {
        return {
            slide: [1, 2, 3, 4, 5, 6],
            swiperOption: {
                loop: true, //无限滚动
                direction: "vertical",  //竖排
                slidesPerView: 1,   //同屏显示数量 可以为auto
                freeMode: true, //滑动模式 false滑动只一格 true根据惯性滑动
                mousewheel: true,   //开启鼠标滚轮控制
                pagination: {
                    el: ".swiper-pagination",
                    clickable: true //分页器（小圆点）选择
                }
            }
        };
    },
    components: { swiper, swiperSlide }
};
</script>

<style scoped>
.swiper-slide {
    height: 4rem;
    text-align: center;
    padding-top: 3rem;
    border-bottom: 1px solid #ccc;
}
</style>