<template>
  <transition name="fade">
    <div class="popup-mask" v-if="visible" @click.self="handleClose">
      <div class="popup-content">
        <slot></slot>
        <button class="popup-close" @click="handleClose">×</button>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'PopupVue',
  props: {
    value: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    visible: {
      get () {
        return this.value
      },
      set (val) {
        this.$emit('input', val)
      }
    }
  },
  methods: {
    handleClose () {
      this.visible = false
    }
  }
}
</script>

<style scoped>
.popup-mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.popup-content {
  background: hsl(36, 100%, 99%);
  padding: 75px 25px 0;
  left: 0;
  position: absolute;
  min-width: 258px;
  height: 100%;
  line-height: 50px;
  font-size: 18px;
}

.popup-close {
  position: absolute;
  top:25px;
  width: 14px;
  height: 15px;
  background: none;
  border: none;
  font-size: none;
  cursor: pointer;
  background: url('../assets/images/icon-close.svg') no-repeat;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
