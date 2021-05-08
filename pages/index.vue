<template>
  <main>
    <div class="a-spacing-large"></div>
    <div class="container-fluid browsing-history">
      <div class="row">
        <div class="col-sm-8 col-8">
          <h1 class="a-size-large a-spacing-none a-text-normal">
            All Products
          </h1>
          <div class="a-spacing-large"></div>
          <nuxt-link to="/products" class="a-button-buy-again"
            >Add to Products</nuxt-link
          >
          <nuxt-link to="/category" class="a-button-history margin-right-10"
            >Add to Category</nuxt-link
          >
          <nuxt-link to="/owner" class="a-button-history margin-right-10"
            >Add to Owner</nuxt-link
          >
        </div>
      </div>
    </div>
    <div class="a-spacing-large"></div>

    <!-- Products box -->
    <div class="container-fluid browsing-history">
      <div class="row">
        <div
          v-for="(product, index) in products"
          :key="product._id"
          class="col-xl-2 col-lg-2 col-md-3 col-sm-6 col-6 br bb"
        >
          <div class="history-box">
            <div class="text-center">
              <a href="#" class="a-link-normal">
                <img :src="product.photo" alt class="img-fluid" />
              </a>
              <div class="a-spacing-top-base asin-title">
                <span class="a-text-normal">
                  <div class="p13n-sc-truncated">{{ product.title }}</div>
                </span>
              </div>
              <div class="a-row">
                <a href="#">
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                </a>
                <span class="a-letter-space"></span>
                <span class="a-color-tertiary a-size-small asin-reviews"
                  >(1234)</span
                >
              </div>
              <div class="a-row">
                <span class="a-size-base a-color-price">
                  <span class="p13n-sc-price">
                    &#8358; {{ product.price }}</span
                  >
                </span>
              </div>
              <div class="a-row">
                <nuxt-link
                  :to="`/products/${product._id} `"
                  class="a-button-history margin-right-10"
                  >Edit</nuxt-link
                >
                <a
                  href="/"
                  class="a-button-history margin-right-10"
                  @click="onDeleteProduct(product._id, index)"
                  >Delete</a
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  // asyncData is a nuxt js function, that run on the server and load before the page finishes whick is good for SEO
  // it is used to fetch Data
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("http://localhost:3000/api/products");
      // console.log(response);
      return {
        products: response.products
      };
    } catch (error) {}
  },
  methods: {
    async onDeleteProduct(id, index) {
      try {
        let response = await this.$axios.$delete(
          `http://localhost:3000/api/product/${id}`
        );
        if (response.status) {
          this.product.splice(index, 1);
        }
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style></style>
