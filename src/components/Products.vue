<template>
  <div class="products">
    <div class="cate">
      <div
        class="cate__item" 
        :class="{ active:cateIndex==cate.id }"
        v-for="cate in cates" :key="cate.id" 
        @click="handleChooseCate(cate.id)"
      >{{ cate.name }}</div>
    </div>
    <div class="product-list">
       <div 
        class="product-list__item"
        v-for="product in filterProducts" 
        :key="'product_'+product.id"
        @click="handleItemClick(product.id)"
      >
        <div class="product-list__item__img">
          <img :src="product.img">
        </div>
        <div class="product-list__item__name">{{ product.name }}</div>
      </div>
    </div>
    <div class="overlay" :class="{ active: isOpen }" @click="handleClosePopUp"></div>
    <div class="choose-product" :class="{ active: isOpen }">
      <div class="choose-product__img">
        <img :src="getChooseProductDetail.img">
      </div>
      <div class="choose-product__detail">
        <p>名称：{{ getChooseProductDetail.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import products from '../product.json'
  export default {
    name: 'products',
    props: {
      searchString: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        isOpen: false, // 打开商品popup
        productIndex: '',
        products,
        cateIndex: 0,
        cates: [
          { id: 0, name: '全部' },
          { id: 1, name: '商品分类1' },
          { id: 2, name: '商品分类2' },
          { id: 3, name: '商品分类3' },
          { id: 4, name: '商品分类4' }
        ]
      }
    },
    computed: {
      filterProducts() {
        let newProducts = [ ...this.products ];
        // 筛选分类
        if(this.cateIndex!=0) {
          newProducts = newProducts.filter(item => item.cate==this.cateIndex);
        }

        // 筛选搜寻关键字
        if(this.searchString!='') {
          newProducts = newProducts.filter(item => item.name.includes(this.searchString));
        }
        return newProducts;
      },
      getChooseProductDetail() {
        const chooseProduct = this.products.filter(item => item.id==this.productIndex);
        if(chooseProduct.length>0) {
          return chooseProduct[0];
        }else{
          return {};
        }
      }
    },
    methods: {
      handleChooseCate(id) {
        console.log('123');
        this.cateIndex = id;
      },
      handleItemClick(id) {
        this.productIndex = id;
        this.isOpen = true;
      },
      handleClosePopUp() {
        this.isOpen = false;
        setTimeout(() => {
          this.productIndex='';
        }, 500);
      }
    }
  }
</script>

<style lang="less" scoped>
.products {
  position: relative;
  .cate {
    position: fixed;
    bottom: 16%;
    left: 40px;
    width: 150px;
    .cate__item {
      width: 100px;
      text-align: center;
      background: white;
      padding: 8px;
      margin-bottom: 5px;
      border: 1px solid #999;
      cursor: pointer;
      &.active {
        background: rgb(70, 110, 219);
        border-color: rgb(70, 110, 219);
        color: white;
      }
    }
  }
  .product-list {
    width: 100%;
    padding-left: 150px;
    display: flex;
    flex-wrap: wrap;
    .product-list__item {
      cursor: pointer;
      flex: 0 0 calc(16.6666% - 16.6666px);
      margin-right: 20px;
      margin-bottom: 20px;
      padding: 20px;
      border-radius: 3px;
      box-shadow: 1px 1px 5px 2px rgba(0,0,0,.2);
      background: white;
      &:nth-child(6n) {
        margin-right: 0;
      }
    }
    .product-list__item__img {
      img {
        width: 100%;
      }
    }
    .product-list__item__name {
      text-align: center;
    }
  }
  .overlay {
    top: 0;
    left: 0;
    position: fixed;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,.5);
    z-index: 100;
    display: none;
    &.active {
      display: block;
    }
  }
  .choose-product {
    left: 15%;
    top: 0%;
    transform: translateY(-100%);
    position: fixed;
    width: 70%;
    background: white;
    z-index: 101;
    max-height: 70%;
    padding: 30px;
    border-radius: 5px;
    text-align: center;
    transition: .5s;
    &.active {
      top: 50%;
      transform: translateY(-50%);
    }
  }
}
</style>