<template>
    <div class="smallCardSwiper">

        <div class="swiper-container smallCardSwiper__container" v-swiper:itemSlider="swiperOption">
            <div class="swiper-wrapper smallCardSwiper__wrapper" ref="swiper">
                <div class="swiper-slide smallCardSwiper__slide"
                     v-for="(item,index) in items"
                     @mouseover="hoverItem(index, 'over')"
                     @mouseout="hoverItem(index, 'out')"
                     @click="hoverItem(index, 'out')"
                     :key="index + 'swipe'">
                    <vue360 :imagePath="item.imagePath"
                            fileName="{index}.png"
                            :amount=item.amount
                            :loop="10"
                            :autoplaySpeed="70"
                            :autoplay="item.autoplay"

                    />
                    <div class="swiper-slide__name">
                        Стул {{index + 1}}
                    </div>
                </div>
            </div>
            <div class="swiper-button-prev"></div>
            <div class="swiper-button-next"></div>

        </div>
        <div class="swiper-pagination"></div>
    </div>

</template>

<script>
    import vue360 from '../vue360';
    import "swiper/dist/css/swiper.min.css";

    export default {
        name: "SmallCardSwiper",
        components: {
            vue360
        },
        props: {
            items: {
                type: Array,
                default() {
                    return []
                }
            },

        },
        mounted() {

        },

        beforeDestroy() {
            this.itemSlider.destroy();
        },
        data() {
            return {

                isShow: false,
                swiperOption: {
                    slidesPerView: 4,
                    spaceBetween: 10,
                    slidesPerGroup: 1,
                    autoHeight: false,

                   //  preventClicksPropagation: false,
                   //  preventClicks: false,
                   // // preventInteractionOnTransition: true,
                   //  allowTouchMove: false,
                   //  nested: true,
                    //touchEventsTarget: '',
                  //  simulateTouch: false,
                   // shortSwipes: false,

                    loop: false,
                    threshold: 15,
                    longSwipesRatio: 0.7,
                    touchStartForcePreventDefault: true,
                    loopFillGroupWithBlank: false,
                    watchOverflow: false,
                    navigation: {
                        nextEl: '.swiper-button-next',
                        prevEl: '.swiper-button-prev'
                    },
                    pagination: {
                        el: '.swiper-pagination',
                        type: 'bullets',
                        clickable: true
                    },
                    on: {
                        init: () => {
                            this.isShow = true;
                        },
                        // slideChange: () => {
                        //   this.activeSlide = this.itemSlider.activeIndex;
                        // }
                    },
                    breakpoints: {
                        // 767: {
                        //     slidesPerView: 1,
                        //     slidesPerGroup: 1
                        // },
                        // 1249: {
                        //     slidesPerView: 'auto',
                        //     slidesPerGroup: 1
                        // },

                    },
                }
            }
        },
        methods: {
            hoverItem(idx, type) {
               this.$emit('hoverItem', {
                   idx: idx,
                   val: type === 'over' ? true : false
               });
            }
        }

    }
</script>

<style lang="scss">
.smallCardSwiper {
    width: 1200px;
    margin: 0 auto;

    text-align: center;

    .swiper-button-prev {
        left: 0;
    }

    .swiper-button-next {
        right: 0;
    }

    .swiper-slide {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .swiper-slide__name {
        margin-top: 15px;
        font-size: 16px;
        color: black;
    }

    .swiper-pagination {
        position: relative;
        margin-top: 15px;
    }

    .swiper-pagination-bullet {
        margin: 0 10px;
    }
}

</style>