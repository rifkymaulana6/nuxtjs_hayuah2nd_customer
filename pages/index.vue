<template>
  <div>
    <Nav/>
    <HomeCarousel :hotItems="hotItems" />
    <br/><br/>
    <v-container>
      <h1 class="text-md-h4 text-h6">Check these out</h1>
      <br/>
      <ProductSlider :products="products" />
      <br/><br/><br/>
    </v-container>
    <Footer/>
    <ScrollTop/>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  async asyncData() {
    const {data} = await axios.get('http://localhost:8000/api/products')
    const {data: hotItems} = await axios.get('http://localhost:8000/api/products/hot-items')
    return {
      products: data,
      hotItems: hotItems
    }
  },
    // async created() {
    //     this.sale_items = await axios.get('http://localhost:8000/api/products').where({ hotItems: true })
    //     this.products = await axios.get('http://localhost:8000/api/products')
    // },
    // data() {
    //     return {
    //         products: null,
    //         sale_items: null
    //     };
    // }
    // async asyncData({ $axios }) {
    //   let { data } = await $axios.get("/products");
    //   return { products: data};
    // }
};
</script>

<style>
  
</style>