<template>
  <div class="app">
    <header>
      <div class="left">
        <button
          type="button"
          class="mobile-only"
          aria-controls="nav-popup"
          aria-label="Open the navigation menu"
          @click="showPopup = true">open nav</button>
        <h1><a href="#">sneakers</a></h1>
      </div>
      <nav>
         <Popup id="nav-popup" v-model="showPopup" class="mobile-only">
          <ul>
            <li><a href="#">Collections</a></li>
            <li><a href="#">Men</a></li>
            <li><a href="#">Women</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
          </ul>
        </Popup>
        <ul class="desktop-only">
          <li><a href="#">Collections</a></li>
          <li><a href="#">Men</a></li>
          <li><a href="#">Women</a></li>
          <li><a href="#">About</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </nav>
      <div class="right">
        <div class="cart">
          <button type="button" class="cart-icon" aria-label="cart button" @click="showCart = true">cart</button>
          <span v-show="cartAll" class="cart-num">{{cartAll}}</span>
        </div>
        <button type="button" class="avatar" aria-label="avatar button">avatar</button>
      </div>
      <CartBox v-model="showCart" :cartAll="cartAll" @clearAll="handleClearAll"></CartBox>
    </header>
    <main>
      <section class="carousel" aria-label="banner">
        <div
          class="carousel-track"
          :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
        >
          <div class="carousel-inner" v-for="(item, index) in bannerList" :key="index">
            <figure class="slide">
              <img :src="item" alt="Men's sports shoe pictures" />
            </figure>
          </div>
        </div>
        <button class="carousel-btn prev" aria-label="previous" @click="prev"></button>
        <button class="carousel-btn next" aria-label="next" @click="next"></button>
      </section>
      <article class="goods-intro" aria-labelledby="goods-name">
        <p class="company">SNEAKER COMPANY</p>

        <h2 id="goods-name">Fall Limited Edition Sneakers</h2>

        <p class="goods-describe">These low-profile sneakers are your perfect casual wear companion. Featuring a
        durable rubber outer sole, they’ll withstand everything the weather can offer.</p>
      </article>
      <section class="product-price" aria-label="price infomation">
        <div class="price">
          <div class="left">
            <div class="dis-price">
              $125.00
            </div>
            <div class="discount">
              50%
            </div>
          </div>
          <div class="original-price">
            $250.00
          </div>
        </div>
        <CountBox :countIndex="countIndex" @handleChange="countIndex = $event"></CountBox>
        <button class="add-cart" type="button" @click="addCart">
          <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg"><path d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z" fill="hsl(220, 13%, 13%)" fill-rule="nonzero"/></svg>
          Add to cart</button>
      </section>
    </main>
  </div>
</template>

<script>
import CountBox from './components/CountBox.vue'
import Popup from './components/Popup.vue'
import CartBox from './components/CartBox.vue'
export default {
  name: 'App',
  components: {
    Popup, CountBox, CartBox
  },
  data () {
    return {
      showCart: false,
      showPopup: false,
      bannerList: [
        require('./assets/images/image-product-1.jpg'),
        require('./assets/images/image-product-2.jpg'),
        require('./assets/images/image-product-3.jpg'),
        require('./assets/images/image-product-4.jpg')
      ],
      currentIndex: 0,
      countIndex: 1,
      cartAll: 0
    }
  },
  mounted () {
    const carousel = this.$el.querySelector('.carousel')

    carousel.addEventListener('wheel', e => {
      if (Math.abs(e.deltaX) > Math.abs(e.deltaY)) {
        e.preventDefault()
      }
    }, { passive: false })

    carousel.addEventListener('touchmove', e => {
      e.stopPropagation()
    }, { passive: false })
  },
  beforeDestroy () {
    this.stopAutoPlay()
  },
  methods: {
    next () {
      this.currentIndex = (this.currentIndex + 1) % this.bannerList.length
    },
    prev () {
      this.currentIndex = (this.currentIndex - 1 + this.bannerList.length) % this.bannerList.length
    },
    startAutoPlay () {
      this.timer = setInterval(() => {
        this.next()
      }, 3000)
    },
    stopAutoPlay () {
      clearInterval(this.timer)
    },
    // 加入购物车
    addCart () {
      this.cartAll = this.cartAll + this.countIndex
      console.log(this.cartAll)
      this.countIndex = 1
    },
    handleClearAll (newValue) {
      this.cartAll = newValue
    }
  }
}
</script>

<style lang="less">
@import '@/styles/index.less';
</style>
