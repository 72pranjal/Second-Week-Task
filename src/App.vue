<template>
  <div id="app">
    <DeskTopHeader :totalProductCount="totalProductCount" />
    <div class="container">
      <ProductContainer v-if="filtersData.length" :dataForFilters="filtersData" :dataForProducts="productsData"
        :dataForSorting="sortingOptions" @handleClickThenActive="getProductOfCurrentPage" @sortData="getSortedData"
        @getFilterString="getFilters" :currentPagination="currentPagination" />
      <DestTopFooter />
    </div>
  </div>
</template>

<script>
import DeskTopHeader from "./components/BaseAppShellHeader/DeskTopHeader.vue";
import ProductContainer from "./components/ProductContainer/ProductContainer.vue";
import DestTopFooter from "./components/BaseAppShellFooter/DestTopFooter.vue";

export default {
  components: {
    DeskTopHeader,
    ProductContainer,
    DestTopFooter,
  },
  data() {
    return {
      productsData: [],
      filtersData: [],
      sortingOptions: [],
      totalProductCount: 0,
      currentPagination: 1,
      sortingValue: "",
      filterSting: "",
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
        this.totalProductCount = response.data.result.count;
      });
    },

    // Function is used to get sorted data from according to selected sorting option
    getSortedDataFromApi() {
      const axios = require("axios");
      const api = `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.currentPagination}&count=20&sort_by=${this.sortingValue}&sort_dir=desc&filter=`;
      axios.get(api).then((response) => {
        this.productsData = response.data.result.products;
      });
    },

    // Function is used to get data of current page from api
    getDataOfCurrentPage() {
      const axios = require("axios");
      const api = `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.currentPagination}&count=20&sort_by=&sort_dir=desc&filter=`;
      axios.get(api).then((response) => {
        this.productsData = response.data.result.products;
      });
    },

    // Function is used to get product data from api accoding to
    // applied filters bt user
    getFiltersData() {
      const axios = require("axios");
      const api = `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.currentPagination}&count=20&sort_by=&sort_dir=desc&filter=${this.filterSting}`;
      axios.get(api).then((response) => {
        this.productsData = response.data.result.products;
      });
    },

    // Function is used to get current page number
    // and get data according to current page
    getProductOfCurrentPage(currentPage) {
      this.currentPagination = currentPage;
      if (this.filterSting) {
        this.getFiltersData();
      } else {
        this.getDataOfCurrentPage();
      }
    },

    // Function is used to check
    // If sorting option is selected then get data according to selected option
    // If sorting option is selected and current page is greater than 1 then send back to
    // first page number with selected sorting option
    getSortedData(sortedValue) {
      this.sortingValue = sortedValue;
      if (this.currentPagination !== 1 && this.sortingValue !== "") {
        this.currentPagination = 1;
      }
      this.getSortedDataFromApi();
    },

    // Function is used check the applied filter array lenght is zero or not
    getFilters(applyFilters) {
      if (applyFilters.length) {
        if (applyFilters.length > 1) {
          let str = "";
          for (let i = 0; i < applyFilters.length; i++) {
            if(!str){
              str = str + applyFilters[i]
            } else {
              str = str + "," + applyFilters[i]
            }
          }
          this.filterSting = str;
        } else {
          this.filterSting = applyFilters[0];
        }
        if (this.currentPagination > 1) this.currentPagination = 1;
        this.getFiltersData();
      } else {
        this.filterSting = ""
        this.getDataOfCurrentPage();
        // this.getProductData();
      }
    },
  },

  mounted() {
    this.getProductData();
  },
};
</script>

<style>
#app {
  background-color: #fff;
  width: 100%;
}
.container {
 padding: 0px 10px;
 font-family: Jost-regular;
}
</style>
