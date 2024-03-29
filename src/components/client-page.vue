<template>
    <div class="app-main">        
        <main-header />
        <main>
            <div class="portfolio">
                <div class="portfolio__bg-wrap">
                    <div class="swiper-container">
                        <div class="swiper-wrapper">
                            <div v-for="(portfolio, index) in portfolios" :key="index" class="swiper-slide">
                                <div class="portfolio__bg-inner">
                                    <div class="portfolio__bg" :style="'background-image: url(/images/visual/'+portfolio.code+'.jpg);'"></div>
                                    <div class="portfolio__caption-wrap">
                                        <div class="container container--lg">
                                            <div class="portfolio__caption">
                                                <p class="txt--lg">{{ portfolio.summary.find(item => item.tit === 'service').txt }}</p>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="portfolio__txt txt--lg">
                                        <p>{{portfolio.txt}}</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="portfolio__blind portfolio__blind--1"></div>
                <div class="portfolio__blind portfolio__blind--2"></div>
                <div class="portfolio__blind portfolio__blind--3"></div>
                <div class="portfolio__blind portfolio__blind--4"></div>
                <span v-show="!intro" class="portfolio__line portfolio__line--1"></span>
                <span v-show="!intro" class="portfolio__line portfolio__line--2"></span>
                <span v-show="!intro" class="portfolio__line portfolio__line--3"></span>
                <div class="portfolio__tit-wrap">
                    <div class="swiper-container" ref="titSwiper">
                        <div class="swiper-wrapper">
                            <div v-for="(portfolio, index) in portfolios" :key="index" class="swiper-slide">
                                <div class="portfolio__tit-inner">
                                    <div class="container container--lg">
                                        <h2 class="portfolio__tit tit--lg"><span>{{portfolio.tit}}</span></h2>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="portfolio__control">
                    <div class="container container--lg">
                        <div class="portfolio__control-inner">
                            <div class="portfolio__control-btn">
                                <button class="portfolio__prev btn btn-icon white"><icon-chevron direction="up" /></button>
                                <button class="portfolio__next btn btn-icon white"><icon-chevron direction="down" /></button>
                                <button class="portfolio__pause btn btn-icon white"><icon-pause /></button>
                                <button class="portfolio__play btn btn-icon white"><icon-play /></button>
                            </div>
                            <div class="portfolio__pagination"></div>
                        </div>
                    </div>
                </div>
                <button class="portfolio__btn" @click="showPortfolioDetails">
                    <div class="portfolio__btn-inner">
                        <span class="portfolio__btn-line portfolio__btn-line--1"></span>
                        <span class="portfolio__btn-line portfolio__btn-line--2"></span>
                        <span class="portfolio__btn-line portfolio__btn-line--3"></span>
                        <span class="portfolio__btn-line portfolio__btn-line--4"></span>
                        <p class="txt">OVERVIEW</p>
                    </div>
                </button>
            </div>
        </main>
        <div v-if="dialog" class="dialog">
            <div class="dialog__inner">
                <div class="dialog__scroll-area" @scroll="handleScroll">
                    <div class="dialog__visual" :style="'background-image: url(/images/dialog/'+selectedPortfolio.code+'.jpg);'">
                        <div class="container">
                            <div class="dialog__visual-inner">
                                <span class="dialog__line dialog__line--1"></span>
                                <span class="dialog__line dialog__line--2"></span>
                                <span class="dialog__line dialog__line--3"></span>
                                <span class="dialog__line dialog__line--4"></span>
                                <span class="dialog__line dialog__line--5"></span>
                                <div class="dialog__blind dialog__blind--1"></div>
                                <div class="dialog__blind dialog__blind--2"></div>
                                <div class="dialog__blind dialog__blind--3"></div>
                                <div class="dialog__blind dialog__blind--4"></div>
                                <div class="dialog__blind dialog__blind--5"></div>
                                <div class="dialog__blind dialog__blind--6"></div>
                                <h3 class="dialog__visual-tit tit">{{ selectedPortfolio.tit }}</h3>
                                <ul class="dialog__summary">
                                    <li v-for="item in selectedPortfolio.summary" :key="item.tit">
                                        <div class="dialog__summary-inner">
                                            <p class="dialog__summary-caption txt--xs">{{item.tit}}</p>
                                            <h5 class="dialog__summary-tit txt">{{item.txt}}</h5>
                                        </div>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="dialog__content">
                        <div class="container">
                            <div class="dialog__content-inner">
                                <div class="dialog__content-left">
                                    <div class="dialog__content-left-inner">
                                        <div class="dialog__content-left-content">
                                            <h4 class="dialog__content-tit tit--sm">{{selectedPortfolio.tit}}</h4>
                                            <div class="dialog__overview txt">
                                                <p class="dialog__overview-tit">OVERVIEW</p>
                                                <p class="dialog__overview-txt">
                                                    {{ selectedPortfolio.txt }}
                                                </p>
                                            </div>                                            
                                            <div class="dialog__btn-group">
                                                <a v-for="item in selectedPortfolio.btn" :key="item.tit" :href="item.link" target="_blank" class="btn btn-arrow">
                                                    <span>{{item.tit}}</span>
                                                    <icon-arrow />
                                                </a>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="dialog__content-right">
                                    <img :src="'/images/screen/'+selectedPortfolio.code+'.jpg'" class="dialog__image" />
                                    <div class="dialog__control">
                                        <div class="dialog__control-left">
                                            <div class="dialog__control-tit">
                                                <icon-arrow direction="left" />
                                                <p class="txt">prev</p>
                                            </div>
                                            <button class="dialog__control-btn" :style="'background-image: url(/images/thumb/'+prevPortfolio.code+'.jpg);'" @click="changePortfolio(-1)">
                                                <div class="dialog__control-btn-logo" :style="'background-image: url(/images/logo/'+prevPortfolio.code+'.svg);'"></div>
                                            </button>
                                        </div>
                                        <div class="dialog__control-right">
                                            <div class="dialog__control-tit">
                                                <p class="txt">next</p>
                                                <icon-arrow />
                                            </div>
                                            <button class="dialog__control-btn" :style="'background-image: url(/images/thumb/'+nextPortfolio.code+'.jpg);'" @click="changePortfolio(+1)">
                                                <div class="dialog__control-btn-logo" :style="'background-image: url(/images/logo/'+nextPortfolio.code+'.svg);'"></div>
                                            </button>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <button v-show="dialog" class="dialog-close btn btn-icon white large" @click="dialogClose"><icon-close /></button>
        <intro-area v-show="intro" />
        <div class="cursor">
            <span class="cursor__default"></span>
            <div class="cursor__slide">
                <div class="swiper-container">
                    <div class="swiper-wrapper">
                        <div v-for="(portfolio, index) in portfolios" :key="index" class="swiper-slide">
                            <div class="cursor__slide-inner" :style="'background-image: url(/images/hover/'+portfolio.code+'.jpg);'"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import MainHeader from "@/components/inc/main-header.vue";
import IntroArea from "@/components/intro-area.vue";
import IconChevron from "@/components/icons/icon-chevron.vue";
import IconPause from "@/components/icons/icon-pause.vue";
import IconPlay from "@/components/icons/icon-play.vue";
import IconClose from "@/components/icons/icon-close.vue";
import IconArrow from "@/components/icons/icon-arrow.vue";

import { portfolios } from "@/assets/data/portfolio.js";

import Swiper from "swiper/bundle";

export default {
    components: {
        MainHeader,
        IntroArea,
        IconChevron,
        IconPause,
        IconPlay,
        IconClose,
        IconArrow,
    },
    data() {
        return {
            portfolios,
            currentIndex: 0,
            dialog: false,
            intro: true,
        };
    },
    mounted() {
        this.init();
        this.handleMouseMove();
        const portfolioBtn = document.querySelector(".portfolio__btn");
        setTimeout(() => {
            this.intro = false;
            portfolioBtn.classList.add("show");
        }, 3990);
    },  
    methods: {
        async init() {
            this.$nextTick(() => {
                setTimeout(() => {

                    // 배경슬라이드
                    var portfolioBg = new Swiper(".portfolio__bg-wrap .swiper-container", {
                        effect: 'fade',
                        slidesPerView : 1,
                        loop: false,
                    });
                    
                    // overview hover 슬라이드
                    var portfolioCursor = new Swiper(".cursor__slide .swiper-container", {
                        effect: "fade",
                        slidesPerView : 1,
                        loop: false,
                    });
                    
                    // 타이틀 슬라이드
                    var portfolioTit = new Swiper(".portfolio__tit-wrap .swiper-container", {
                        effect: 'fade',
                        slidesPerView : 1,
                        mousewheel: {
                            releaseOnEdges: true,
                        },
                        autoplay: {
                            delay: 5000,
                            disableOnInteraction: false,
                        },
                        speed: 0,
                        loop: false,
                        touchRatio: 0,
                        pagination: {
                            el: ".portfolio__pagination",
                            clickable: true,
                            renderBullet: function(index, className) {
                                const number = (index + 1 < 10) ? '0' + (index + 1) : (index + 1);
                                return '<span class="' + className + '">' + number + '</span>';
                            },
                        },
                        navigation: {
                            nextEl: ".portfolio__next",
                            prevEl: ".portfolio__prev",
                        },
                        thumbs: {
                            swiper: portfolioCursor,
                        },
                        on: {
                            activeIndexChange: this.handleActiveIndexChange
                        },
                    });

                    // 슬라이드 연동
                    portfolioTit.controller.control = portfolioBg;
                    portfolioBg.controller.control = portfolioTit;

                    // 슬라이드 정지, 시작
                    const portfolio = document.querySelector(".portfolio");
                    const portfolioStop = document.querySelectorAll(".portfolio__pause, .portfolio__btn");
                    const portfolioPlay = document.querySelectorAll(".portfolio__play, .dialog-close");
                    
                    portfolioTit.autoplay.stop();
                    setTimeout(() => {
                        portfolioTit.autoplay.start();
                    }, 3500);
                    
                    portfolioStop.forEach(portfolioStop => {
                        portfolioStop.addEventListener("click", () => {
                            portfolioTit.autoplay.stop();
                            portfolio.classList.add("stop");
                        });
                    });
                    portfolioPlay.forEach(portfolioPlay => {
                        portfolioPlay.addEventListener("click", () => {
                            portfolioTit.autoplay.start();
                            portfolio.classList.remove("stop");
                        });
                    });
                }, 10);
            });
        },        

        // 슬라이드 방향 감지
        handleActiveIndexChange(swiper) {
            const currentIndex = swiper.activeIndex;                                
            const previousIndex = swiper.previousIndex;
            const portfolio = document.querySelector(".portfolio");
            if (currentIndex < previousIndex) {
                portfolio.classList.remove("down", "up");
                setTimeout(() => {
                    portfolio.classList.add("down");
                }, 10);
            } else if (currentIndex > previousIndex) {
                portfolio.classList.remove("down", "up");
                setTimeout(() => {
                    portfolio.classList.add("up");
                }, 10);
            }
            this.currentIndex = currentIndex;
        },

        // 팝업, 팝업 내용 바인딩
        showPortfolioDetails() {
            this.dialog = true;
            const html = document.querySelector("html");
            setTimeout(() => {
                html.classList.add("open");
            }, 10);
        },
        
        changePortfolio(step) {
            let newIndex = this.currentIndex + step;
            const numPortfolios = this.portfolios.length;
            if (newIndex < 0) {
                newIndex = numPortfolios - 1;
            } else if (newIndex >= numPortfolios) {
                newIndex = 0;
            }
            this.currentIndex = newIndex;
            const scrollArea = document.querySelector(".dialog__scroll-area");
            scrollArea.scrollTop = 0;
            const dialog = document.querySelector(".dialog");
            dialog.classList.add("scroll", "scroll-top");
            setTimeout(() => {
                dialog.classList.remove("scroll");
            }, 100);
            
            const swiperInstance = this.$refs.titSwiper.swiper;
            swiperInstance.slideTo(newIndex);
        },

        // 팝업 닫힘
        dialogClose(){
            const html = document.querySelector("html");
            const dialog = document.querySelector(".dialog");
            const dialogCloseBtn = document.querySelector(".dialog-close");
            setTimeout(() => {
                html.classList.remove("open");
                dialog.classList.remove("scroll-top");
            }, 10);    
            setTimeout(() => {
                this.dialog = false;
                const scrollArea = document.querySelector(".dialog__scroll-area");
                scrollArea.scrollTop = 0
            }, 350);         
            dialogCloseBtn.classList.remove('black');
            dialogCloseBtn.classList.add('white');
        },

        // 커서
        handleMouseMove() {
            window.addEventListener('mousemove', (event) => {
                var client_x = event.clientX;
                var client_y = event.clientY;
                const cursor = document.querySelector('.cursor');
                cursor.style.top = client_y + 'px';
                cursor.style.left = client_x + 'px'; 
                const elements = document.querySelectorAll('button, a, .swiper-pagination-bullet');
                elements.forEach(element => {
                    element.addEventListener('mouseenter', () => {
                        document.querySelector('.cursor').classList.add('active');
                    });
                    element.addEventListener('mouseleave', () => {
                        document.querySelector('.cursor').classList.remove('active');
                    });
                });                
                const portfolioBtn = document.querySelector(".portfolio__btn");
                portfolioBtn.addEventListener('mouseenter', () => {
                    document.querySelector('.cursor').classList.add('slide');
                });
                portfolioBtn.addEventListener('mouseleave', () => {
                    document.querySelector('.cursor').classList.remove('slide');
                });
            });
        },
        
        // 팝업 스크롤이벤트
        handleScroll() {
            const scrollArea = document.querySelector(".dialog__scroll-area");
            const scrollWrap = document.querySelector(".dialog__inner");
            const dialogCloseBtn = document.querySelector(".dialog-close");

            if (scrollArea.scrollTop > 480) {
                scrollWrap.classList.add('active');
            } else {
                scrollWrap.classList.remove('active');
            }

            if (scrollArea.scrollTop > 292) {
                dialogCloseBtn.classList.remove('white');
                dialogCloseBtn.classList.add('black');
            } else {
                dialogCloseBtn.classList.remove('black');
                dialogCloseBtn.classList.add('white');
            }
        },
    },

    // 팝업 내용 바인딩
    computed: {
        selectedPortfolio() {
            return this.portfolios[this.currentIndex];
        },
        
        prevPortfolio() {
            const prevIndex = this.currentIndex === 0 ? this.portfolios.length - 1 : this.currentIndex - 1;
            return this.portfolios[prevIndex];
        },
        
        nextPortfolio() {
            const nextIndex = this.currentIndex === this.portfolios.length - 1 ? 0 : this.currentIndex + 1;
            return this.portfolios[nextIndex];
        },
    }
};
</script>
