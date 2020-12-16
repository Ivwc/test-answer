

<template>
    <div class="banner-container" ref="carousel" :style="{ height: carouselWidth/900*300+'px' }">
      <ul class="images" :style="{
        width:sliderArray.length*100+'%',
        marginLeft:-index*100+'%'
      }">
        <li v-for="(item,i) of sliderArray" :key="i" :style="{ width: carouselWidth+'px' }">
          <a href="javascript:void(0)"><img :src="item.img" :style="{ width: carouselWidth+'px' }"></a>
        </li>
      </ul>
      <ul class="dots">
        <li v-for="(item,i) of sliderArray" 
          :class="{
            active:i===index
          }" :key="i"
          @click="handleIndex(i)"
        ></li>
      </ul>
    </div>
</template>

<script>
const sliderArray = [
  {
    img: 'https://picsum.photos/900/300?image=1081',
    href: "#"
  },
  {
    img: 'https://picsum.photos/900/300?image=1068',
    href: "#"
  },
  {
    img: 'https://picsum.photos/900/300?image=1084',
    href: "#"
  }
];
export default {
    name: "Slider",
  data(){
      return{
        index:0,
        sliderArray,
        carouselWidth: 1080
      }
  },
  mounted() {
    this.$nextTick(() => {
      this.carouselWidth = this.$refs.carousel.parentNode.clientWidth;
    })
  },
  methods: {
    handleIndex(i) {
      this.index = i;
    }
  }
}
</script>

<style scoped>
  ul {
    padding: 0;
    margin: 0;
  }
  .banner-container {
    /* height: 350px; */
    position: relative;
    overflow: hidden;
  }
  .banner-container li {
    display: block;
    /* width: 1080px; */
    height: 100%;
    float: left;
  }
  .images {
    height: 100%;
    transition: 0.5s;
  }
  .banner-container img {
    /* width: 1080px; */
    height: 100%;
    display: block;
  }
  .dots {
    position: absolute;
    bottom: 10px;
    right: 10px;
    display: flex;
  }
  .dots li {
    width: 10px;
    cursor: pointer;
    height: 10px;
    margin: 0 3px;
    border-radius: 50%;
    border: 1px solid;
    color: #fff;
  }
  .dots li.active {
    background: #fff;
  }
</style>