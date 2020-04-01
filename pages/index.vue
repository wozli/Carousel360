<template>
    <div class="container">
        <div class="swiper360" ref="swiper">
            <div class="swiper360__container" v-if="activeSwiper">

                <div class="swiper360__item"
                     v-for="(item, index) in items"
                     :key="index"
                     @click="actionSwiper(item.step, index)"
                     :class="{'current': item.step === 3,
                              'next': item.step === 4,
                              'next-next': item.step === 5,
                              'prev': item.step === 2,
                              'prev-prev': item.step === 1,
                              'flight' : runSwiper}">

                    <vue360 :imagePath="item.imagePath"
                            fileName="{index}.png"
                            :amount=item.amount
                            :loop="0"
                            :id="item.id"
                            @changeActiveImg="item.starImg = $event - 1"
                            :autoplay="item.autoplay"
                            :spinReverse="item.spinReverse"
                            :activeImg="item.starImg"
                            :toImg="handlerActiveImg(item.step)"
                            :toImgActive="true"
                    />
                </div>

            </div>

        </div>

        <hr>
        <variantOne :items="items2"/>
        <hr>
        <variantTwo :items="items3" @hoverItem="hoverItem($event)"/>
        <!--<button type="button" @click="start()">-->
        <!--Повернуть-->
        <!--</button>-->

    </div>
</template>

<script>
    import vue360 from '~/components/vue360.vue'
    import variantOne from '~/components/swipers/variant1'
    import variantTwo from '~/components/swipers/variant2'

    export default {
        components: {
            vue360,
            variantOne,
            variantTwo,
        },
        mounted() {
            this.handlerSwiper();
        },

        data() {
            return {
                activeSwiper: false,
                activeImg: 1,
                runSwiper: false,
                items: [
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 15,
                        step: 1,
                        amount: 37,
                        id:1,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/two',
                        autoplay: false,
                        starImg: 26,
                        step: 2,
                        amount: 36,
                        id:2,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 0,
                        step: 3,
                        amount: 37,
                        id:3,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/three',
                        autoplay: false,
                        starImg: 11,
                        step: 4,
                        amount: 37,
                        id:4,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 22,
                        step: 5,
                        amount: 37,
                        id:5,
                    }
                ],
                items2: [
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 15,
                        step: 1,
                        amount: 37,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/two',
                        autoplay: false,
                        starImg: 26,
                        step: 2,
                        amount: 36,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 0,
                        step: 3,
                        amount: 37,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/three',
                        autoplay: false,
                        starImg: 11,
                        step: 4,
                        amount: 37,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 22,
                        step: 5,
                        amount: 37,
                    }
                ],
                items3: [
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 15,
                        step: 1,
                        amount: 37,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/two',
                        autoplay: false,
                        starImg: 26,
                        step: 2,
                        amount: 36,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 0,
                        step: 3,
                        amount: 37,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/three',
                        autoplay: false,
                        starImg: 11,
                        step: 4,
                        amount: 37,
                    },
                    {
                        spinReverse: false,
                        imagePath: '/chair/one',
                        autoplay: false,
                        starImg: 22,
                        step: 5,
                        amount: 37,
                    }
                ],
            }
        },

        methods: {
            hoverItem(e) {

                this.items3[e.idx].autoplay = e.val;
            },

            handlerActiveImg(step) {

                let newActiveImg = 0;
                switch (step) {
                    case 1:
                        newActiveImg = 15;
                        break;
                    case 2:
                        newActiveImg = 26;
                        break;
                    case 3:
                        newActiveImg = 0;
                        break;
                    case 4:
                        newActiveImg = 11;
                        break;
                    case 5:
                        newActiveImg = 22;
                        break;
                }
                return newActiveImg
            },

            handlerSwiper() {

                this.activeSwiper = true;
            },
            actionSwiper(step, index) {

                if (step === 4) {


                    this.runSwiper = true;
                    this.items.forEach((item, idx) => {
                        item.spinReverse = true;
                        let exit = this.handlerActiveImg(item.step === 1 ? 5 : item.step - 1);

                        if (item.starImg > exit) {
                            if (item.starImg - exit >= item.amount - item.starImg + exit) {
                                item.spinReverse = false;
                            } else {
                                item.spinReverse = true;
                            }
                        } else {
                            if (exit - item.starImg >= item.amount - exit + item.starImg) {
                                item.spinReverse = true;
                            } else {
                                item.spinReverse = false;
                            }
                        }

                        if (item.step === 1) {
                            item.step = 5;

                        } else {

                            item.step--;
                        }

                        item.autoplay = true;

                    });

                    setTimeout(() => {
                        this.disabelAutoplay();
                    }, 1101);

                }

                if (step === 2) {

                    this.runSwiper = true;
                    this.items.forEach((item, idx) => {
                        item.spinReverse = false;
                        let exit = this.handlerActiveImg(item.step === 5 ? 1 : item.step + 1);

                        if (item.starImg > exit) {
                            if (item.starImg - exit >= item.amount - item.starImg + exit) {
                                item.spinReverse = false;
                            } else {
                                item.spinReverse = true;
                            }
                        } else {
                            if (exit - item.starImg >= item.amount - exit + item.starImg) {
                                item.spinReverse = true;
                            } else {
                                item.spinReverse = false;
                            }
                        }

                        if (item.step === 5) {

                            item.step = 1;
                        } else {

                            item.step++;
                        }

                        item.autoplay = true;
                    });
                    setTimeout(() => {
                        this.disabelAutoplay();
                    }, 1101);
                }
            },

            disabelAutoplay() {
                this.items.forEach((item, idx) => {
                    item.autoplay = false;
                });
                this.runSwiper = false;
            }

        }
    }
</script>

<style lang="scss">


    .swiper360 {
        width: 100%;
        display: flex;
        justify-content: center;
        height: 420px;

        &__container {
            position: relative;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        &__item {
            width: 320px;
            position: absolute;
            transition: transform 1.1s;

            & > div {
                pointer-events: none;
            }

            &.current {
                z-index: 5;
                transform: translate(0%, 0%);

                & > div {
                    pointer-events: inherit;
                }
            }

            &.next {
                z-index: 4;
                transform: scale(0.7) translate(140%, -10%);
            }

            &.next-next {
                z-index: 3;
                transform: scale(0.5) translate(130%, -30%);
            }

            &.prev {
                z-index: 4;
                transform: scale(0.7) translate(-140%, -10%);
            }

            &.prev-prev {
                z-index: 3;
                transform: scale(0.5) translate(-130%, -30%);
            }

            &.flight {
                pointer-events: none;
            }
        }

    }
</style>
