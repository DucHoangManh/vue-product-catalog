<template>
  <div>
    <div class="d-flex align-items-center flex-column ml-5 mb-5">
      <h4>Product: {{ productNumber }}</h4>
      <h4>Product On Sale: {{ productOnSale }}</h4>
      <h4>Total Price: {{ totalPrice }}</h4>
      <h4>Average Price: {{ avgPrice }}</h4>
      <div class="d-flex justify-content-around">
        <select
          class="form-control"
          aria-label="Default select example"
          @change="onOptionChange"
        >
          <option selected>Sort by</option>
          <option value="1">Price (Lowest first)</option>
          <option value="2">Price (Highest first)</option>
          <option value="3">Name (A-Z)</option>
          <option value="4">Name (Z-A)</option>
        </select>
        <input
          type="text"
          class="form-control ml-1"
          placeholder="Search product..."
          aria-label="Search field"
          aria-describedby="basic-addon1"
          @keyup="onSearchChange"
        />
      </div>
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
          image: 'https://plclagi.com/wp-content/uploads/2020/11/00-8.jpg',
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
      return this.formatPrice(
        this.productList.reduce((sum, p2) => {
          return sum + p2.price
        }, 0)
      )
    },
    avgPrice: function() {
      return this.formatPrice(
        this.productList.reduce((sum, p2) => {
          return sum + p2.price
        }, 0) / this.productList.length
      )
    },
  },
  methods: {
    sortByPriceLowest() {
      this.productList.sort((p1, p2) => {
        return p1.price - p2.price
      })
    },
    sortByPriceHighest() {
      this.productList.sort((p1, p2) => {
        return p2.price - p1.price
      })
    },
    sortByName() {
      this.productList.sort((p1, p2) => {
        return p1.name.localeCompare(p2.name)
      })
    },
    sortByNameReverse() {
      this.productList
        .sort((p1, p2) => {
          return p1.name.localeCompare(p2.name)
        })
        .reverse()
    },
    onSearchChange(e) {
      let re = new RegExp(e.target.value, 'i')
      this.productList = this.productListOrigin.filter((p) => {
        return p.name.match(re)
      })
    },
    formatPrice(num) {
      const formatter = new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2,
      })
      return formatter.format(num)
    },
    onOptionChange(e) {
      if (e.target.value === '1') {
        this.sortByPriceLowest()
      } else if (e.target.value === '2') {
        this.sortByPriceHighest()
      } else if (e.target.value === '3') {
        this.sortByName()
      } else if (e.target.value === '4') {
        this.sortByNameReverse()
      }
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
  margin-top: 2%;
}
</style>
