<template>
    <div class="app-main">        
        <main-header></main-header>
        <main>
            <div class="protfolio">
                <div class="protfolio__bg-wrap">
                    <div class="swiper-container">
                        <div class="swiper-wrapper">
                            <div v-for="(item, index) in protfolio" :key="index" class="swiper-slide">
                                <div class="protfolio__bg-inner">
                                    <div class="protfolio__bg" :style="'background-image: url(images/visual/'+item.code+'.jpg);'"></div>
                                    <div class="protfolio__caption-wrap">
                                        <div class="container container--lg">
                                            <div class="protfolio__caption">
                                                <p>{{item.caption}}</p>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="protfolio__txt">
                                        <p>{{item.txt}}</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="protfolio__blind protfolio__blind--1"></div>
                <div class="protfolio__blind protfolio__blind--2"></div>
                <div class="protfolio__blind protfolio__blind--3"></div>
                <div class="protfolio__blind protfolio__blind--4"></div>
                <span class="protfolio__line protfolio__line--1"></span>
                <span class="protfolio__line protfolio__line--2"></span>
                <span class="protfolio__line protfolio__line--3"></span>
                <div class="protfolio__tit-wrap">
                    <div class="swiper-container">
                        <div class="swiper-wrapper">
                            <div v-for="(item, key) in protfolio" :key="key" class="swiper-slide">
                                <div class="protfolio__tit-inner">
                                    <div class="container container--lg">
                                        <h2 class="protfolio__tit"><span>{{item.tit}}</span></h2>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="protfolio__control">
                    <div class="container container--lg">
                        <div class="protfolio__control-inner">
                            <div class="protfolio__control-btn">
                                <button class="protfolio__prev btn btn-icon white"><icon-chevron direction="up" /></button>
                                <button class="protfolio__next btn btn-icon white"><icon-chevron direction="down" /></button>
                                <button class="protfolio__pause btn btn-icon white"><icon-pause /></button>
                                <button class="protfolio__play btn btn-icon white"><icon-play /></button>
                            </div>
                            <div class="protfolio__pagination"></div>
                        </div>
                    </div>
                </div>
                <button class="protfolio__btn"><span>OVERVIEW</span></button>
                <div class="protfolio__details">{{ currentIndex }}</div>
                <div class="cursor">
                    <span class="cursor__default"></span>
                    <div class="cursor__slide">
                        <div class="swiper-container">
                            <div class="swiper-wrapper">
                                <div v-for="(item, index) in protfolio" :key="index" class="swiper-slide">
                                    <div class="cursor__slide-inner" :style="'background-image: url(images/hover/'+item.code+'.jpg);'"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>
</template>

<script>

import MainHeader from "@/components/inc/main-header.vue";
import IconChevron from "@/components/icons/icon-chevron.vue";
import IconPause from "@/components/icons/icon-pause.vue";
import IconPlay from "@/components/icons/icon-play.vue";

import { protfolio } from "@/assets/data/protfolio.js";

import Swiper from "swiper/bundle";

export default {
    components: {
        MainHeader,
        IconChevron,
        IconPause,
        IconPlay,
    },
    data() {
        return {
            protfolio,
            currentIndex: 0,
        };
    },
    mounted() {
        this.init();
    },  
    methods: {
        async init() {
            this.$nextTick(() => {
                setTimeout(() => {
                    var protfolioTit = new Swiper(".protfolio__tit-wrap .swiper-container", {
                        on: {
                            activeIndexChange: this.handleActiveIndexChange
                        },
                    });
                }, 10);
            });
        },
        handleActiveIndexChange(swiper) {
            const currentIndex = swiper.activeIndex;                                
            const previousIndex = swiper.previousIndex;
            const protfolio = document.querySelector(".protfolio");
            if (currentIndex < previousIndex) {
                protfolio.classList.remove("down", "up");
                setTimeout(() => {
                    protfolio.classList.add("down");
                }, 10);
            } else if (currentIndex > previousIndex) {
                protfolio.classList.remove("down", "up");
                setTimeout(() => {
                    protfolio.classList.add("up");
                }, 10);
            }
            this.currentIndex = currentIndex; // Update currentIndex when activeIndex changes
        },
    },
};
</script>
