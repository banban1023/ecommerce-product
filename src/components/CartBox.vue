<template>
  <div class="cart-mask" v-if="value" @click.self="handleClose">
    <div class="cart-box">
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
.cart-mask {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
  .cart-box {
    width: 361px;
    height: 257px;
    background-color: #fff;
    position: absolute;
    top: 76px;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 10px;
    h2 {
      padding: 25px;
      height: 69px;
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
</style>
