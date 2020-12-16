<template>
  <div id="app">
    <SearchBar :searchString.sync="searchString"/>
    <Carousel/>
    <CountDown/>
    <Products :searchString="searchString"/>
    <GotoTop/>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue'
import Carousel from './components/Carousel.vue'
import CountDown from './components/CountDown.vue'
import Products from './components/Products.vue'
import GotoTop from './components/GotoTop.vue'

export default {
  name: 'App',
  components: {
    SearchBar,Carousel,CountDown,Products,GotoTop
  },
  data() {
    return {
      searchString: ''
    }
  },
}
</script>

<style lang="less">
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 40px;
  background: #ddd;
}

#app {
  // padding-top: 66px;
  position: relative;
  width: 90%;
}


</style>
