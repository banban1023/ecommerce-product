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
            <li v-for="(item, index) in navItems" :key="index"><a href="#">{{item}}</a></li>
          </ul>
        </Popup>
        <ul class="desktop-only">
          <li
           v-for="(item, index) in navItems"
           :key="index"
           :class="{active: currentNavIndex === index}"
           @click="currentNavIndex = index"
          ><a href="#">{{item}}</a></li>
        </ul>
      </nav>
      <div class="right">
        <div class="cart">
          <button type="button" class="cart-icon" aria-label="cart button" @click="showCart = true">cart</button>
          <span v-show="cartAll" class="cart-num">{{cartAll}}</span>
          <CartBox class="cart-box" v-model="showCart" :cartAll="cartAll" @clearAll="handleClearAll"></CartBox>
        </div>
        <button type="button" class="avatar" aria-label="avatar button">avatar</button>
      </div>
    </header>
    <main>
      <div class="desktop-left">
        <section class="carousel" aria-label="banner">
          <div
            class="carousel-track"
            :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
          >
            <div class="carousel-inner" @click="openLightbox(index)" v-for="(item, index) in bannerList" :key="index">
              <figure class="slide">
                <img :src="item" alt="Men's sports shoe pictures" />
              </figure>
            </div>
          </div>
          <button class="carousel-btn prev" aria-label="previous" @click="prev"></button>
          <button class="carousel-btn next" aria-label="next" @click="next"></button>
        </section>
        <section class="small-carousel">
          <button class="small-goods" v-for="(item, index) in bannerList" :key="index"
            :class="{active: currentIndex === index}"
            @click="switchImage(index)"
          >
            <img :src="item" alt="goods-img">
          </button>
        </section>
      </div>
      <section class="desktop-msg">
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
          <div class="btn">
            <CountBox :countIndex="countIndex" @handleChange="countIndex = $event"></CountBox>
            <button class="add-cart" type="button" @click="addCart">
              <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg"><path d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z" fill="hsl(220, 13%, 13%)" fill-rule="nonzero"/></svg>
              Add to cart</button>
          </div>
        </section>
      </section>
    </main>
    <div class="lightbox" v-if="showLightbox" @click.self="closeLightbox">
        <div class="lightbox-content">
          <button class="close-btn" @click="closeLightbox" aria-label="Close lightbox">
            <svg width="14" height="15" xmlns="http://www.w3.org/2000/svg">
              <path d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z" fill="#fff" fill-rule="evenodd"/>
            </svg>
          </button>
          <div class="lightbox-main">
            <div
              class="lightbox-track"
              :style="{ transform: `translateX(-${lightboxIndex * 100}%)` }"
            >
              <div
                class="lightbox-slide"
                v-for="(item, index) in bannerList"
                :key="index"
              >
                <img :src="item" alt="Men's sports shoe pictures" />
              </div>
            </div>
          </div>
          <button class="lightbox-prev" @click.stop="lightboxPrev" aria-label="Previous image">
              <svg width="12" height="18" xmlns="http://www.w3.org/2000/svg">
                <path d="M11 1 3 9l8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd"/>
              </svg>
            </button>
            <button class="lightbox-next" @click.stop="lightboxNext" aria-label="Next image">
              <svg width="13" height="18" xmlns="http://www.w3.org/2000/svg">
                <path d="m2 1 8 8-8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd"/>
              </svg>
            </button>
          <div class="lightbox-thumbnails">
            <button
              v-for="(item, index) in bannerList"
              :key="index"
              :class="{active: lightboxIndex === index}"
              @click.stop="lightboxIndex = index"
            >
              <img :src="item" alt="Thumbnail">
            </button>
          </div>
        </div>
      </div>
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
      showLightbox: false, //
      lightboxIndex: 0, //
      navItems: ['Collections', 'Men', 'Women', 'About', 'Contact'],
      bannerList: [
        require('./assets/images/image-product-1.jpg'),
        require('./assets/images/image-product-2.jpg'),
        require('./assets/images/image-product-3.jpg'),
        require('./assets/images/image-product-4.jpg')
      ],
      currentIndex: 0,
      countIndex: 1,
      cartAll: 0,
      currentimgIndex: 0,
      currentNavIndex: null
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
    // 打开大图预览
    openLightbox (index) {
      this.lightboxIndex = index
      this.showLightbox = true
      document.body.style.overflow = 'hidden' // 防止背景滚动
    },

    // 关闭大图预览
    closeLightbox () {
      this.showLightbox = false
      document.body.style.overflow = ''
    },

    // 大图预览上一张
    lightboxPrev () {
      this.lightboxIndex = (this.lightboxIndex - 1 + this.bannerList.length) % this.bannerList.length
    },

    // 大图预览下一张
    lightboxNext () {
      this.lightboxIndex = (this.lightboxIndex + 1) % this.bannerList.length
    },
    switchImage (index) {
      this.currentIndex = index
      this.currentimgIndex = index
    },
    next () {
      this.currentIndex = (this.currentIndex + 1) % this.bannerList.length
      this.currentimgIndex = this.currentIndex
    },
    prev () {
      this.currentIndex = (this.currentIndex - 1 + this.bannerList.length) % this.bannerList.length
      this.currentimgIndex = this.currentIndex
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
