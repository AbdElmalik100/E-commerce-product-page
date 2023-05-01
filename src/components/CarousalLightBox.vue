<template>
    <div class="overlay position-fixed">
        <div class="light-box-carousal d-flex flex-column align-items-center">
            <svg @click="$emit('close-light-box')" class="close" xmlns="http://www.w3.org/2000/svg" width="14" height="15">
                <path
                    d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z"
                    fill="#69707D" fill-rule="evenodd" />
            </svg>
            <div class="main-pic position-relative">
                <div class="prev position-absolute" @click="prev">
                    <svg xmlns="http://www.w3.org/2000/svg" width="12" height="18">
                        <path d="M11 1 3 9l8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd" />
                    </svg>
                </div>
                <img class="rounded-3" width="425" :src="`/src/assets/images/image-product-${defaultNum}.jpg`" alt="">
                <div class="next position-absolute" @click="next">
                    <svg xmlns="http://www.w3.org/2000/svg" width="13" height="18">
                        <path d="m2 1 8 8-8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd" />
                    </svg>
                </div>
            </div>
            <div class="pags d-flex align-items-center gap-3 mt-3">
                <div :class="`cont rounded-3 ${(index + 1) === defaultNum ? 'active' : ''}`" v-for="(item, index) in images"
                    :key="index" @click="slider(index + 1)">
                    <img class="rounded-3 img-fluid" width="70" :src="item" alt="">
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
const props = defineProps(['images', 'mainDefault'])
const defaultNum = ref(props.mainDefault)

let slider = (num) => {
    defaultNum.value = num
}

let prev = () => {
    defaultNum.value--
    if (defaultNum.value < 1) {
        defaultNum.value = props.images.length
    }
}
let next = () => {
    defaultNum.value++
    if (defaultNum.value > props.images.length) {
        defaultNum.value = 1
    }
}

</script>
<style lang="scss" scoped>
@import '../global';

.overlay {
    top: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.75);
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;

    .light-box-carousal {
        .close {
            align-self: flex-end;
            margin-bottom: 15px;
            cursor: pointer;

            path {
                transition: 0.2s;
                fill: $White;
            }

            &:hover path {
                fill: $Orange;
            }
        }

        &>img {
            cursor: pointer;
        }

        .main-pic {
            user-select: none;

            .prev,
            .next {
                width: 50px;
                height: 50px;
                display: flex;
                align-items: center;
                justify-content: center;
                border-radius: 50%;
                top: 50%;
                transform: translateY(-50%);
                background-color: white;
                cursor: pointer;

                path {
                    transition: 0.2s;
                }
                &:hover {
                    svg path {
                        stroke: $Orange;
                    }
                }
            }

            .prev {
                left: -25px;
                svg {
                    margin-right: 5px;
                }
            }
            
            .next {
                right: -25px;
                svg {
                    margin-left: 5px;
                }
            }
        }

        .pags {
            .cont {
                cursor: pointer;
                border: 3px solid transparent;
                transition: 0.2s;
                position: relative;

                &::before {
                    content: '';
                    position: absolute;
                    width: 100%;
                    height: 100%;
                    border: 2px solid transparent;
                    border-radius: 10px;
                    transition: 0.2s;
                    left: 0;
                    top: 0;
                }

                &:hover::before {
                    background-color: #ffffffa6;
                }

                &.active::before {
                    border-color: $Orange;
                    background-color: #ffffffa6;
                }
            }
        }
    }
}
</style>