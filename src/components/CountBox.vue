<template>
  <div class="count-box">
    <button type="button" aria-label="add goods">+</button>
    <span>{{count}}</span>
    <button type="button" aria-label="reduce goods">-</button>
  </div>
</template>

<script>
export default {
  props: {
    countIndex: {
      type: Number,
      required: true
    }
  }
}
</script>

<style lang="less" scoped>
.count-box {

}
</style>
