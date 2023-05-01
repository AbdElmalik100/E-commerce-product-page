<template>
  <main class="min-vh-100 pb-5">
    <NavHeader :cart="cart" @del-cart="del"></NavHeader>
    <div class="container mt-5">
      <div class="cont d-flex align-items-center justify-content-between">
        <div class="carousal d-flex flex-column">
          <div class="position-relative" style="cursor: pointer;">
            <div class="prev d-none position-absolute" @click="prev">
              <svg xmlns="http://www.w3.org/2000/svg" width="12" height="18">
                <path d="M11 1 3 9l8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd" />
              </svg>
            </div>
            <img @click="lightBox = true" class="rounded-4" width="475"
              :src="`/src/assets/images/image-product-${defaultNum}.jpg`" alt="">
            <div class="next d-none position-absolute" @click="next">
              <svg xmlns="http://www.w3.org/2000/svg" width="13" height="18">
                <path d="m2 1 8 8-8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd" />
              </svg>
            </div>
          </div>
          <div class="pagination d-flex align-items-center gap-3 mt-4">
            <div :class="`rounded-4 wrapper ${(index + 1) === defaultNum ? 'active' : ''}`"
              v-for="(item, index) in images" :key="index" @click="slider(index + 1)">
              <img class="rounded-4 img-fluid" width="100" :src="item" alt="">
            </div>
          </div>
        </div>
        <div class="right-side w-50">
          <h4 class="text-uppercase fs-6 fw-bold">Sneaker Company</h4>
          <h1 class="fw-bold my-4 w-75">Fall Limited Edition Sneakers</h1>
          <p>These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole,
            they'll withstand everything the weather can offer.</p>
          <div class="price my-5">
            <h2 class="fw-bold">${{ pirce }}</h2>
            <span class="text-decoration-line-through fw-bold">$250.00</span>
          </div>
          <div class="buttons d-flex align-items-center gap-4">
            <div class="amount p-3 px-4 justify-content-between rounded-3 d-flex align-items-center">
              <svg @click="decreaseAmount" class="minus" xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink" width="12" height="4">
                <defs>
                  <path
                    d="M11.357 3.332A.641.641 0 0 0 12 2.69V.643A.641.641 0 0 0 11.357 0H.643A.641.641 0 0 0 0 .643v2.046c0 .357.287.643.643.643h10.714Z"
                    id="a" />
                </defs>
                <use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#a" />
              </svg>
              <span class="fw-bold">{{ amount }}</span>
              <svg @click="increaseAmount" class="plus" xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink" width="12" height="12">
                <defs>
                  <path
                    d="M12 7.023V4.977a.641.641 0 0 0-.643-.643h-3.69V.643A.641.641 0 0 0 7.022 0H4.977a.641.641 0 0 0-.643.643v3.69H.643A.641.641 0 0 0 0 4.978v2.046c0 .356.287.643.643.643h3.69v3.691c0 .356.288.643.644.643h2.046a.641.641 0 0 0 .643-.643v-3.69h3.691A.641.641 0 0 0 12 7.022Z"
                    id="b" />
                </defs>
                <use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#b" />
              </svg>
            </div>
            <button class="p-3 px-5 rounded-3" @click="addToCart">
              <svg xmlns="http://www.w3.org/2000/svg" width="22" height="20">
                <path
                  d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z"
                  fill="#69707D" fill-rule="nonzero" />
              </svg>
              Add To Cart
            </button>
          </div>
        </div>
        <CarousalLightBox v-if="lightBox" :mainDefault="defaultNum" :images="images"
          @close-light-box="() => lightBox = false"></CarousalLightBox>
      </div>
    </div>
  </main>
</template>
<script setup>
import NavHeader from './components/NavHeader.vue';
import CarousalLightBox from './components/CarousalLightBox.vue'
import { ref } from 'vue'


const defaultNum = ref(1)
const lightBox = ref(false)
const images = [
  '../public/images/image-product-1-thumbnail.jpg',
  '/src/assets/images/image-product-2-thumbnail.jpg',
  '/src/assets/images/image-product-3-thumbnail.jpg',
  '/src/assets/images/image-product-4-thumbnail.jpg',
]
const amount = ref(0)
const pirce = ref('125.00')
const cart = ref('')

let slider = (num) => {
  defaultNum.value = num
}

let increaseAmount = () => {
  amount.value++
}
let decreaseAmount = () => {
  if (amount.value <= 0) {
    return
  } else amount.value--
}

let addToCart = () => {
  cart.value = amount.value
  if (amount.value === 0) {
    cart.value = ''
  }
}

let del = () => {
  cart.value = ''
}


// At Media (767px)
let prev = () => {
  defaultNum.value--
  if (defaultNum.value < 1) {
    defaultNum.value = images.length
  }
}
let next = () => {
  defaultNum.value++
  if (defaultNum.value > images.length) {
    defaultNum.value = 1
  }
}

</script>
<style lang="scss">
@import './global';

* {
  box-sizing: border-box;
}

body {
  font-family: 'Kumbh Sans', sans-serif;
  background-color: $White;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

p {
  font-size: 16px;
}

.container {
  .carousal {
    &>img {
      cursor: pointer;
    }

    .pagination {
      .wrapper {
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
          border-radius: 15px;
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

  .right-side {
    h4 {
      color: $Orange;
    }

    h1 {
      color: $veryDarkBlue;
    }

    p {
      color: $darkGrayishBlue;
      line-height: 1.8;
    }

    .price {
      h2 {
        color: $veryDarkBlue;
        position: relative;

        &::before {
          content: '50%';
          position: absolute;
          font-weight: bold;
          font-size: 15px;
          left: 135px;
          top: 50%;
          padding: 5px 10px;
          border-radius: 5px;
          transform: translateY(-50%);
          background-color: $paleOrange;
          color: $Orange;
        }
      }

      span {
        color: $grayishBlue;
      }
    }

    .buttons {
      user-select: none;

      .amount {
        background-color: $lightGrayishBlue;
        width: 200px;

        .minus,
        .plus {
          cursor: pointer;
          transition: 0.2s;

          &:hover {
            opacity: 0.5;
          }
        }

        span {
          color: $veryDarkBlue;
        }
      }

      button {
        border: none;
        background-color: $Orange;
        color: $White;
        text-transform: uppercase;
        display: flex;
        align-items: center;
        transition: 0.2s;

        &:hover {
          opacity: 0.7;
        }

        svg {
          margin-right: 10px;

          path {
            fill: $White;
          }
        }
      }
    }
  }

  @media (max-width: 991px) {
    .cont {
      flex-direction: column;
    }

    .right-side {
      width: 100% !important;
      margin-top: 50px;
    }
  }

  @media (max-width: 767px) {
    margin-top: 0 !important;
    padding-left: 0 !important;
    padding-right: 0 !important;

    .carousal {

      .prev,
      .next {
        display: block !important;
        top: 50%;
        transform: translateY(-50%);
        background-color: $White;
        border-radius: 50%;
        width: 50px;
        height: 50px;
        display: flex !important;
        align-items: center;
        justify-content: center;
      }

      .prev {
        left: 20px;

        svg {
          margin-right: 5px;
        }
      }

      .next {
        right: 20px;

        svg {
          margin-left: 5px;
        }
      }

      &>div img {
        width: 100%;
        border-radius: 0 !important;
        pointer-events: none;
      }

      .pagination {
        display: none !important;
      }
    }

    .right-side {
      padding-left: 20px !important;
      padding-right: 20px !important;
    }

    .price {
      display: flex;
      align-items: center;
      justify-content: space-between;

      h2 {
        &::before {
          left: 100px !important;
        }
      }
    }

    .buttons {
      flex-direction: column;

      .amount,
      button {
        width: 100% !important;
      }

      button {
        justify-content: center;
      }
    }
  }
}
</style>