<template>
  <div class="card col-md-4" style="width: 18rem;">
    <div class="p-image">
      <img
        class="card-img-top mx-auto rounded"
        :src="item.image"
        alt="Card image cap"
      />
    </div>
    <div class="card-body d-flex flex-column align-items-center">
      <h5 class="card-title mx-auto">{{ item.name }}</h5>
      <div class="d-flex flex-row justify-content-around">
        <p v-if="!item.sale_price" class="card-text mx-auto">
          {{ displayPrice }}
        </p>
        <p v-if="item.sale_price" class="card-text mx-auto mr-5">
          <del> {{ displayPrice }} </del>
        </p>
        <p v-if="item.sale_price" class="card-text mx-auto">
          , sale price: {{ displaySalePrice }}
        </p>
      </div>
      <a href="#" class="btn btn-primary mx-auto">Add to cart</a>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Product',
  props: {
    item: Object,
  },
  computed: {
    displayPrice() {
      return this.formatPrice(this.item.price)
    },
    displaySalePrice() {
      return this.formatPrice(this.item.sale_price)
    },
  },
  methods: {
    formatPrice(num) {
      const formatter = new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2,
      })
      return formatter.format(num)
    },
  },
}
</script>
<style scoped>
.p-image {
  max-width: 100%;
}
</style>
