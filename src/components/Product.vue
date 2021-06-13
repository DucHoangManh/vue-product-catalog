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
          {{ item.price }}$
        </p>
        <p v-if="item.sale_price" class="card-text mx-auto mr-5">
          <del> {{ item.price }}$ </del>
        </p>
        <p v-if="item.sale_price" class="card-text mx-auto">
          , sale price: {{ item.sale_price }}$
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
}
</script>
<style scoped>
.p-image {
  height: 300px;
  width: 100%;
}
</style>
