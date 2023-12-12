<script setup>
import  { Swiper, SwiperSlide } from 'swiper/vue';


import firstSlide from '../assets/img/first-slide.jpg'
import secondSlide from '../assets/img/second-slide.jpg'
import thirdSlide from '../assets/img/third-slide.jpg'
import fourthSlide from '../assets/img/fourth-slide.jpg'
import fifthSlide from '../assets/img/fifth-slide.jpg'

import { Pagination, Navigation } from 'swiper/modules';


import 'swiper/scss';
import 'swiper/scss/navigation';
import 'swiper/scss/pagination';

const carousel = [{img: firstSlide}, {img: secondSlide}, {img: thirdSlide}, {img: fourthSlide}, {img: fifthSlide}]
</script>

<template>
    <div class="carousel">
        <div class="carousel__top">
            <h2 class="carousel__title">Корпоративная жизнь</h2>
            <button class="swiper-button-next"></button>
		    <button class="swiper-button-prev"></button>
        </div>    
        <swiper
            :modules="[
                Pagination,
                Navigation
            ]"
            :pagination="{
                dynamicBullets: false,
                el: '.carousel__pagination',
                bulletClass: 'swiper-pagination-my-bullet',
                bulletActiveClass: 'swiper-pagination-my-bullet-active',
            }"
            :navigation="{
                nextEl: '.swiper-button-next',
                prevEl: '.swiper-button-prev'
            }"

            class="mySwiper"
        >
        
            <swiper-slide
                :slides-per-view="1"
                :space-between="50"
                v-for="(slide, index) in carousel" :key="index"
            >
                <img :src="slide.img" alt="slide" class="slide__img">
            </swiper-slide>
        </swiper>
        <div class="carousel__pagination"></div>
    </div>
</template>

<style lang="scss">
.carousel {
    margin-top: 103px;
    padding: 0 70px;
    width: 100%;
    position: relative;
    &__top {
        margin-bottom: 55px;
    }
    &__title {
        color: #444;
        font-family: Proxima Nova Condensed;
        font-size: 56px;
        font-style: normal;
        font-weight: 600;
        line-height: 100%; 
    }
    &__pagination{
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        gap: 10px;
        width: 100%;
        margin-top: 28px;
    }
}

.swiper-pagination-my-bullet {
    width: 100%;
    height: 6px;
    display: inline-block;
    border-radius: 0;
    opacity: 0.1;
    background: #000;
    transition: 0.2s background, 0.2s opacity;
}
.swiper-pagination-my-bullet-active {
    background: #A30C33;
    opacity: 1;
}

.slidePrev-btn {
    background: #000;
    height: 50px;
    width: 100px;
}
.swiper-button-next {
    border: none;
    border-radius: 50%;
    width: 56px;
    height: 56px;
    top: 24px;
    right: 70px;
    content: url('../assets/icons/next.png');
}
.swiper-button-prev {
    border: none;
    border-radius: 50%;
    width: 56px;
    height: 56px;
    top: 24px;
    left: 1048px;
    content: url('../assets/icons/prev.png');
}
</style>