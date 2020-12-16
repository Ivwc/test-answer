<template>
  <div class="search-bar" id="searchBar">
    <div class="search-bar__item">
      <Icon icon="search" class="search-btn icon-btn"/>
      <input type="text" class="search-bar__input" :value="searchString" @keyup="handleKeyUp">
      <Icon 
        icon="cancel" 
        class="cancel-btn icon-btn" 
        v-if="searchString!=''"
        @click="handleCleanSearch"
      />
    </div>
  </div>
</template>

<script>
import Icon from './Icon.vue'
  
  export default {
    name: 'search-bar',
    props: {
      searchString: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        
      }
    },
    components: {
      Icon
    },  
    mounted() {
      this.$nextTick(() => {
        window.onscroll = function() {myFunction()};

        // Get the header
        var header = document.getElementById("searchBar");

        // Get the offset position of the navbar
        var sticky = header.offsetTop;

        // Add the sticky class to the header when you reach its scroll position. Remove "sticky" when you leave the scroll position
        function myFunction() {
          if (window.pageYOffset > sticky) {
            header.classList.add("sticky");
          } else {
            header.classList.remove("sticky");
          }
        }
      })
    },
    methods: {
      handleCleanSearch() {
        this.$emit('update:searchString','');
      },
      handleKeyUp(e) {
        this.$emit('update:searchString',e.target.value);
      }
    }
  }
</script>

<style lang="less" scoped>
.search-bar {
  width: 100%;
  padding: 14px;
  position: relative;
  background: #bbb;
  top: 0;
  left: 0;
  &.sticky {
    width: calc((100% - 80px)*0.9);
    position: fixed;
    top: 0;
    left: 40px;
    z-index: 10;
  }
  .icon-btn {
    width: 26px;
    position: absolute;
    top: 0;
    &.search-btn {
      top: 50%;
      transform: translateY(-50%);
      left: 22px;
    }
    &.cancel-btn {
      top: 50%;
      transform: translateY(-50%);
      right: 22px;
    }
  }
  .search-bar__input {
    width: 100%;
    border: 1px solid #ccc;
    font-size: 1.3rem;
    padding: 6px 40px;
    border-radius: 5px;
  }
}
</style>