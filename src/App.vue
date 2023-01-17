<template>
  <div id="app">
    <DeskTopHeader />
    <ProductContainer v-if="filtersData.length" :dataForFilters="filtersData" :dataForProducts="productsData"
      :dataForSorting="sortingOptions" @handleClickThenActive="getValue" @sortData="getSortedData"
      :currentPagination="currentPagination" />
  </div>
</template>

<script>
import DeskTopHeader from "./components/BaseAppShellHeader/DeskTopHeader.vue";
import ProductContainer from "./components/ProductContainer/ProductContainer.vue";

export default {
  components: {
    DeskTopHeader,
    ProductContainer,
  },
  data() {
    return {
      productsData: [],
      filtersData: [],
      sortingOptions: [],
      currentPagination: 1,
      sortingValue: "",
    };
  },
  methods: {
    getProductData() {
      const axios = require("axios");
      const api = `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.currentPagination}&count=20&sort_by=${this.sortingValue}&sort_dir=desc&filter=`;
      axios.get(api).then((response) => {
        console.log(response);
        this.productsData = response.data.result.products;
        this.filtersData = response.data.result.filters;
        this.sortingOptions = response.data.result.sort;
      });
    },

    // Function is used to get current page number
    getValue(currentPage) {
      this.currentPagination = currentPage;
    },

    getSortedData(sortedValue) {
      console.log("hey", sortedValue);
      this.sortingValue = sortedValue;
    },
  },
  mounted() {
    this.getProductData();
  },
  watch: {
    currentPagination() {
      this.getProductData();
    },
    sortingValue() {
      if (this.currentPagination !== 1 && this.sortingValue !== "") {
        this.currentPagination = 1;
      }
      this.getProductData();
    },
  },
};
</script>

<style>
#app {
  background-color: #ffffff;
}
</style>
