<template>
  <div class="goto-top" @click="handleScrollToTop">
    Top
  </div>
</template>

<script>
  export default {
    name: 'goto-top',
    methods: {
      handleScrollToTop() {
        window.scrollTo({'behavior': 'smooth', 'top': 0})
      }
    }
  }
</script>

<style lang="less" scoped>
.goto-top {
  width: 44px;
  height: 44px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgb(64, 136, 224);
  position: fixed;
  bottom: 30px;
  right: 30px;
  color: white;
  border-radius: 100px;
  cursor: pointer;
}
</style>