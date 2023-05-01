<template>
    <header class="header mx-5 py-4 d-flex align-items-center justify-content-between">
        <div class="left-side d-flex align-items-center gap-5">
            <img @click="openMenu = true" class="menu d-none" src="../assets/images/icon-menu.svg" alt="">
            <img src="../assets/images/logo.svg" alt="">
            <div class="overlay"></div>
            <ul :class="`d-flex align-items-center gap-4 ${openMenu ? 'open' : ''}`">
                <img @click="openMenu = false" class="close d-none" src="../assets/images/icon-close.svg" alt="">
                <li>Collections</li>
                <li>Men</li>
                <li>Women</li>
                <li>About</li>
                <li>Contact</li>
            </ul>
        </div>
        <div class="right-side d-flex align-items-center gap-5">
            <div :data-cart="cart" class="cart-cont position-relative" @click="popupOpen = !popupOpen">
                <svg class="cart" xmlns="http://www.w3.org/2000/svg" width="22" height="20">
                    <path
                        d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
                        fill="#69707D" fill-rule="nonzero" />
                </svg>
                <CartPopup v-if="popupOpen" :cart="cart" class="cart-popup" @del-cart="$emit('del-cart')"></CartPopup>
            </div>
            <img width="50" src="../assets/images/image-avatar.png" alt="">
        </div>
    </header>
</template>
<script setup>
import CartPopup from './CartPopup.vue';
import { ref } from 'vue';

defineProps(['cart'])
defineEmits(['del-cart'])
const popupOpen = ref(false)
const openMenu = ref(false)


</script>
<style lang="scss" scoped>
@import '../global';

header {

    border-bottom: 1px solid $grayishBlue;

    .left-side {

        ul {

            li {
                color: $darkGrayishBlue;
                position: relative;
                cursor: pointer;

                &::before {
                    content: '';
                    position: absolute;
                    transition: 0.2s;
                    height: 5px;
                    width: 0%;
                    left: 50%;
                    transform: translateX(-50%);
                    bottom: -37px;
                    background-color: $Orange;
                }

                &:hover::before {
                    width: 100%;
                }

                &:hover {
                    color: $Black;
                }
            }
        }
    }

    .right-side {
        user-select: none;

        .cart-popup {
            position: absolute;
            right: -100px;
            top: 55px;
        }

        img,
        .cart,
        .cart path {
            transition: 0.2s;
            cursor: pointer;
        }

        .cart-cont {
            position: relative;

            &::before {
                content: attr(data-cart);
                position: absolute;
                display: block;
                border-radius: 50px;
                color: $White;
                background-color: $Orange;
                padding: 0px 10px;
                font-weight: bold;
                font-size: 10px;
                left: 8px;
                top: -3px;
            }

            .cart {
                &:hover path {
                    fill: $Black;
                }
            }
        }

        img {
            border: 2px solid transparent;
            border-radius: 50%;

            &:hover {
                border-color: $Orange;
            }
        }
    }

    @media (max-width: 767px) {
        padding-left: 25px;
        padding-right: 25px;
        margin-left: 0px !important;
        margin-right: 0px !important;

        .close {
            display: block !important;
            position: absolute;
            top: 30px;
            left: 25px;
        }

        .left-side {
            gap: 15px !important;

            .menu {
                display: block !important;
            }

            .overlay {
                position: fixed;
                display: none;
                width: 100%;
                height: 100%;
                left: 0;
                top: 0;
                background-color: rgba(0, 0, 0, 0.26);
                z-index: 1000;
            }

            ul {
                transform: translateX(-100%);
                position: fixed;
                flex-direction: column;
                align-items: flex-start !important;
                left: 0;
                top: 0;
                background: white;
                height: 100%;
                z-index: 55555555;
                transition: 0.2s;
                width: 60%;
                padding: 75px 30px;

                li {
                    color: $Black;
                    font-weight: bold;
                }

                &.open {
                    transform: translateX(0);
                }
            }
        }

        .right-side {
            gap: 15px !important;

            img {
                width: 35px;
            }
        }

        .cart-popup {
            right: -67px !important;
            width: 385px;
            top: 65px !important;
            z-index: 5;
        }
    }
}</style>