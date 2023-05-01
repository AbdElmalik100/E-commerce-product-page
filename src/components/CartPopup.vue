<template>
    <div class="cart-popup rounded">
        <div class="cart-cont">
            <span class="d-block fw-bold p-3 border-bottom">Cart</span>
            <div class="item d-flex align-items-center justify-content-center p-3">
                <div v-if="cart > 0" class="d-flex align-items-center flex-column gap-4 flex-fill">
                    <div class="d-flex align-items-center gap-2 justify-content-between w-100">
                        <img width="50" class="rounded-3" src="../../public/images/image-product-1-thumbnail.jpg" alt="">
                        <div class="info">
                            <h6 class="mb-0">Fall Limited Edition Sneakers</h6>
                            <span>$125.00 x {{ cart }}</span> <span class="total ms-2 text-black fw-bold">${{ cart *
                                125 }}.00</span>
                        </div>
                        <img @click="$emit('del-cart')" class="del" width="15" src="../../public/images/icon-delete.svg" alt="">
                    </div>
                    <button class="p-3 border-0 fw-bold w-100 rounded-3">Checkout</button>
                </div>
                <span v-else class="d-block fw-bold">Your cart is empty.</span>
            </div>
        </div>
    </div>
</template>
<script setup>
const props = defineProps(['cart'])


</script>
<style lang="scss" scoped>
@import '../global';

.cart-popup {
    width: 350px;
    background-color: $White;
    box-shadow: 2px 5px 15px #999999;

    .item {
        min-height: 200px;

        span {
            color: $darkGrayishBlue;
        }

        .info {
            h6 {
                color: $darkGrayishBlue;
            }
        }

        .del {
            cursor: pointer;
        }

        button {
            background-color: $Orange;
            color: $White;
            transition: 0.2s;

            &:hover {
                opacity: 0.7;
            }
        }
    }
}</style>