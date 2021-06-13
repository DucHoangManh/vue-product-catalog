<template>
  <div>
    <div d-flex mr-5>
      <h3>Product: {{ productNumber }}</h3>
      <h3>Product On Sale: {{ productOnSale }}</h3>
      <h3>Total Price: {{ totalPrice }}</h3>
      <h3>Average Price: {{ avgPrice }}</h3>
      <input
        type="text"
        class="form-control mr-5 ml-5"
        placeholder="Search product..."
        aria-label="Search field"
        aria-describedby="basic-addon1"
        @keyup="onSearchChange"
      />
      <a href="#" class="btn btn-primary mx-auto mb-5 " @click="sortByPrice"
        >Sort by price</a
      >
    </div>
    <div class="container row mx-auto ">
      <product
        class="col-md-4"
        v-for="product in productList"
        :key="product.id"
        :item="product"
      />
    </div>
  </div>
</template>

<script>
import Product from './components/Product.vue'
export default {
  name: 'App',
  components: {
    Product,
  },
  data() {
    return {
      productListOrigin: [
        {
          id: 1,
          name: 'Red Blue flight',
          price: 67,
          sale_price: null,
          image:
            'http://residencestyle.com/wp-content/uploads/2020/11/abstract-painting.jpg',
        },
        {
          id: 2,
          name: 'Oil lamp',
          price: 10,
          sale_price: null,
          image:
            'https://lh3.googleusercontent.com/proxy/Clr8XWbr3EUJNTvmLFeEoRVxpVqtb0Z68tEBUXah6kv2S_kAHTRKHzxP4vj6ibq7fxdrH-t_kKEdeXrR98RCTgPrkyHpRVoA1zaJJMyKb_Yjp82ef3y-NuY5GQw',
        },
        {
          id: 3,
          name: 'An old call',
          price: 245,
          sale_price: 222,
          image:
            'https://cdn.shopify.com/s/files/1/0012/6287/8783/products/Screen_Shot_2018-11-17_at_10.45.25_AM_grande.png?v=1571725941',
        },
        {
          id: 4,
          name: 'Black bicycle',
          price: 69,
          sale_price: 50,
          image:
            'https://www.antiquetrader.com/.image/t_share/MTc1MjYyODgyODA2NjM4NDA0/1888highwheeltest.jpg',
        },
        {
          id: 5,
          name: 'Heirloom painting',
          price: 368,
          sale_price: null,
          image:
            'https://sarasotaantiquebuyers.com/wp-content/uploads/2014/11/Antique-Oil-Paintings.jpg',
        },
        {
          id: 6,
          name: 'Record player',
          price: 90,
          sale_price: null,
          image: 'https://sc04.alicdn.com/kf/HTB1ds0OSpXXXXX8XXXXq6xXFXXXU.jpg',
        },
      ],
      productList: [],
    }
  },
  mounted: function() {
    this.productList = this.productListOrigin
  },
  computed: {
    productNumber: function() {
      return this.productList.length
    },
    productOnSale: function() {
      return this.productList.filter((p) => {
        return p.sale_price
      }).length
    },
    totalPrice: function() {
      return this.productList.reduce((sum, p2) => {
        return sum + p2.price
      }, 0)
    },
    avgPrice: function() {
      return (
        this.productList.reduce((sum, p2) => {
          return sum + p2.price
        }, 0) / this.productList.length
      )
    },
  },
  methods: {
    sortByPrice() {
      this.productList.sort((p1, p2) => {
        return p1.price - p2.price
      })
    },
    onSearchChange(e) {
      let re = new RegExp(e.target.value)
      this.productList = this.productListOrigin.filter((p) => {
        return p.name.match(re)
      })
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
