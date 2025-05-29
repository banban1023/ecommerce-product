<template>
  <div class="cart-wrapper">
    <div class="cart-mask" v-if="value" @click.self="handleClose"></div>
    <div class="cart-box" v-if="value">
      <h2>Cart</h2>
      <div class="cart-content">
        <p class="null" v-if="cartAll === 0">Your cart is empty.</p>
        <section class="visiable" v-else>
          <div class="goods">
            <img src="../assets/images/image-product-1-thumbnail.jpg" alt="goods picture">
            <div class="info">
              <p class="name">Fall Limited Edition Sneakers</p>
              <span class="price">$125.00</span>
              <span class="count"> x {{cartAll}}</span>
              <span class="total-price">${{totalPrice.toFixed(2)}}</span>
            </div>
            <button aria-label="delete" type="button" class="delete" @click="deleteGoods">delete button</button>
          </div>
          <button class="checkout">Checkout</button>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CartCard',
  props: {
    value: {
      type: Boolean,
      required: true
    },
    cartAll: {
      type: Number,
      required: true
    }
  },
  methods: {
    handleClose () {
      this.$emit('input', false)
    },
    deleteGoods () {
      this.$emit('clearAll', 0)
    }
  },
  computed: {
    totalPrice () {
      return this.cartAll * 125
    }
  }
}
</script>

<style lang="less" scoped>
.cart-wrapper {
  .cart-mask {
    position: absolute;
    left: -100vw;
    top: -52px;
    width: 200vw;
    height: 90vh;
    z-index: 15;
  }
  .cart-box {
    z-index: 30;
    width: 361px;
    height: 257px;
    background-color: #fff;
    border-radius: 10px;
    h2 {
      padding: 25px;
      height: 69px;
      top: 0;
      left: 250px;
      border-bottom: 1px solid hsla(220, 14%, 75%, 0.4);
      font-size: 16px;
    }
    .cart-content {
      padding: 25px;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 188px;
      color: @Dark-grayish-blue;
      font-weight: 700;
      .visiable {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        width: 100%;
        height: 100%;
        .goods {
          display: flex;
          justify-content: space-between;
          height: 51px;
          img {
            width: 51px;
            height: 51px;
          }
          .delete {
            width: 14px;
            height: 16px;
            border: none;
            align-self: center;
            font-size: 0;
            background: url('../assets/images/icon-delete.svg') no-repeat;
          }
        }
        .checkout {
          width: 100%;
          background-color: @Orange;
          height: 56px;
          border-radius: 10px;
          border: none;
          font-size: 16px;
          font-weight: 700;
          color: @Very-dark-blue;
        }
        .info {
          font-weight: normal;
          line-height: 25px;
          .count {
            margin-right: 8px;
          }
          .total-price {
            font-weight: 800;
            color: #000;
          }
        }
      }
    }
  }
}
@media (min-width: 768px) {
  .cart-wrapper {
    .cart-box {
      box-shadow:
      -5px 5px 10px 0 rgba(0, 0, 0, 0.1), /* 左边阴影 */
      5px 5px 10px 0 rgba(0, 0, 0, 0.1),  /* 右边阴影 */
      0 5px 10px 0 rgba(0, 0, 0, 0.1);   /* 下边阴影 */;
    }
  }
}
</style>
