<template>
    <div>
        <div class="search-bar">
            <van-row>
                <van-col span="3"><img :src="locationIcon" width="100%"></van-col>
                <van-col span="16">
                    <input type="text" class="search-input">
                </van-col>
                <van-col span="5">查找</van-col>
            </van-row>
        </div>

        <div class="swiper-area">
            <van-swipe :autoplay="1000">
                <van-swipe-item v-for="(banner, index) in bannerPicArray" :key='index'>
                    <img v-lazy="banner.image" width="100%" />
                </van-swipe-item>
            </van-swipe>
        </div>

        <div class="type-bar">
            <div v-for="(cate,index) in category" :key="index">
                <img v-lazy="cate.image" width="90%" />
                <span>{{cate.mallCategoryName}}</span>
            </div>
        </div>

        <div class="ad-banner">
            <img v-lazy="adBanner.PICTURE_ADDRESS" width="100%">
        </div>

        <div class="recommend-area">
            <div class="recommend-title">
                商品推荐
            </div>
            <div class="recommend-body">
                <swiper :options="swiperOption">
                    <swiper-slide v-for="(item, index) in recommendGoods" :key="index">
                        <div class="recommend-item">
                            <img :src="item.image" width="80%">
                            <div>{{item.goodsName}}</div>
                            <div>￥{{item.price}} (￥{{item.mallPrice}})</div>
                        </div>
                    </swiper-slide>
                </swiper>
            </div>
        </div>

        <floor-component :floorData="floor1" :floorTitle="floorName.floor1"></floor-component>
        <floor-component :floorData="floor2" :floorTitle="floorName.floor1"></floor-component>
        <floor-component :floorData="floor3" :floorTitle="floorName.floor1"></floor-component>

        <!-- <swiperDefault></swiperDefault> -->
    </div>
</template>

<script>
import axios from "axios";
// import swiperDefault from "../swiper/swiperDefault";
import "swiper/dist/css/swiper.css";
import { swiper, swiperSlide } from "vue-awesome-swiper";
import floorComponent from '../component/floorComponent'

export default {
    components: { swiper, swiperSlide, floorComponent },
    data() {
        return {
            locationIcon: require("./../../assets/images/location.png"),
            category: [],
            adBanner: "",
            bannerPicArray: [],
            recommendGoods: [],
            floor1: [],
            floor2: [],
            floor3: [],
            floorName: {},
            swiperOption: {
                loop: true, //无限滚动
                freeMode: true //滑动模式 false滑动只一格 true根据惯性滑动
            }
        };
    },
    created() {
        axios({
            url:
                " https://www.easy-mock.com/mock/5afe6b616c661f4c19ec5312/smilevue/",
            method: "get"
        })
            .then(res => {
                console.log(res);
                if (res.status == 200) {
                    this.category = res.data.data.category;
                    this.adBanner = res.data.data.advertesPicture;
                    this.bannerPicArray = res.data.data.slides;
                    this.recommendGoods = res.data.data.recommend;
                    this.floor1 = res.data.data.floor1; //楼层1数据
                    this.floor2 = res.data.data.floor2; //楼层2数据
                    this.floor3 = res.data.data.floor3; //楼层3数据

                    this.floorName = res.data.data.floorName;
                }
            })
            .catch(err => {});
    }
};
</script>

<style scoped>
.search-bar {
    height: 2.2rem;
    background-color: #e5017d;
    line-height: 2.2rem;
}

.search-input {
    width: 100%;
    height: 1.3rem;
    border-top: 0px;
    border-left: 0px;
    border-right: 0px;
    border-bottom: 1px solid 1px !important ;
    background-color: #e5017d;
    color: #fff;
}

.location-icon {
    padding-top: 0.2rem;
    padding-left: 0.3rem;
}

.swiper-area {
    width: 20rem;
    clear: both;
    overflow: hidden;
}

.type-bar {
    background-color: #fff;
    margin: 0 0.3rem 0.3rem 0.3rem;
    border-radius: 0.3rem;
    font-size: 14px;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
}

.type-bar div {
    padding: 0.3rem;
    font-size: 12px;
    text-align: center;
}

.recommend-area {
    background-color: #fff;
    margin-top: 0.3rem;
}

.recommend-title {
    border-bottom: 1px solid #eee;
    font-size: 14px;
    padding: 0.2rem;
    color: #e5017d;
}

.recommend-body {
    border-bottom: 1px solid #eee;
}

.recommend-item {
    width: 99%;
    border-right: 1px solid #eee;
    font-size: 12px;
    text-align: center;
}
</style>
