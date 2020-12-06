<template>
  <div id="app">
    <div class="tools">
      <AddProduct @add="addProduct" :propsData="product" />
    </div>
    <div class="table">
      <b-table striped hover :fields="header" :items="product" :dark="darkMode">
        <template #cell(action)="row">
          <b-button size="sm" class="mr-1" @click="info(row)">
            編輯
          </b-button>
          <b-button size="sm" class="mr-1">
            刪除
          </b-button>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
import AddProduct from '@/components/add-product'
// 編輯的Component
// 父傳子
// 刪除的Component
export default {
  name: 'App',
  components: {
    AddProduct
  },
  data() {
    return {
      darkMode: false,
      product: [
        {
          id: 0,
          name: '鬼滅之刃潮T',
          size: 'L', //XS超小 S小 M中等 L大 XL超大
          price: 799,
          amount: 10
        }
      ],
      header: [
        {key:'name',label:'商品名稱'},
        {key:'size',label:'尺寸'},
        {key:'price',label:'價格'},
        {key:'amount',label:'數量'},
        {key:'action',label:'動作'},
      ]
    }
  },
  methods: {
    addProduct(productData) {
      this.product.push(productData)
    },
    info(data) {
      console.log(data)
    }
  },
}
</script>

<style lang="scss">
#app {
  .tools {
    padding-top: 30px;
    padding-right: 30px;
    display: flex;
    justify-content: flex-end;
  }
  .table {
    padding: 30px;
  }
}
</style>
