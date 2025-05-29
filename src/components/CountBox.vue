<template>
  <div class="count-box">
    <button type="button" aria-label="reduce goods" class="reduce" @click="changeNum(-1)"></button>
    <span>{{countIndex}}</span>
    <button type="button" aria-label="add goods" class="add" @click="changeNum(1)"></button>
  </div>
</template>

<script>
export default {
  props: {
    countIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    changeNum (num) {
      if (this.countIndex > 1) {
        this.$emit('handleChange', this.countIndex + num)
      } else if (this.countIndex === 1 && num > 0) {
        this.$emit('handleChange', this.countIndex + num)
      }
    }
  }
}
</script>

<style lang="less" scoped>
.count-box {
  width: 100%;
  height: 56px;
  background-color: @Light-grayish-blue;
  display: flex;
  margin: 25px 0 18px;
  border-radius: 10px;
  button {
    background-color: transparent;
    border: none;
    width: 62px;
    height: 100%;
  }
  .reduce {
    background: url('../assets/images/icon-minus.svg') no-repeat center;
  }
  .add {
    background: url('../assets/images/icon-plus.svg') no-repeat center;
  }
  span {
    flex: 1;
    text-align: center;
    line-height: 56px;
    font-weight: 700;
  }
}
@media (min-width: 768px) {
  .count-box {
    margin: 0;
  }
}
</style>
