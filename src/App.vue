<template>
  <div id="app">
    <DeskTopHeader />
    <ProductContainer
    v-if="filtersData.length"
    :dataForFilters="filtersData"
    :dataForProducts="productsData"
    :dataForSorting="sortingOptions"
     />
  </div>
</template>

<script>
import DeskTopHeader from './components/BaseAppShellHeader/DeskTopHeader.vue';
import ProductContainer from './components/ProductContainer/ProductContainer.vue';

export default {
  components: {
    DeskTopHeader,
    ProductContainer
  },
  data() {
    return {
      productsData: [],
      filtersData: [],
      sortingOptions: []
    }
  },
  methods: {
    getProductData() {
      const axios = require("axios")
      axios.get("https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter=")
        .then(response => {
          console.log(response)
          this.productsData = response.data.result.products;
          this.filtersData = response.data.result.filters;
          this.sortingOptions = response.data.result.sort;
          console.log(this.productsData)
        })
    },  
  },
  mounted() {
    this.getProductData();
  }
}
</script>

<style>
#app {
  background-color: #FFFFFF;
}
</style>
