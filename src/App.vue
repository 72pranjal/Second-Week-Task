<template>
  <div id="app">
    <DeskTopHeader :totalProductCount="totalProductCount" :currentPagination="currentPagination"
      @showStory="showOurStory" />
    <div>
      <LoaderFordata :spinLoader="spinLoader" />
      <div v-if="!showStoryData" class="container">
        <ProductContainer v-if="filtersData.length" :dataForFilters="filtersData" :dataForProducts="productsData"
          :dataForSorting="sortingOptions" @handleClickThenActive="getProductOfCurrentPage" @sortData="getSortedData"
          @getFilterString="getFilters" :currentPagination="currentPagination" :totalpageNumber="totalpageNumber" />
      </div>
      <div v-else>
        <OurStory />
      </div>
      <DeskTopFooter />
    </div>
  </div>
</template>

<script>
import DeskTopHeader from "./components/BaseAppShellHeader/DeskTopHeader.vue";
import ProductContainer from "./components/ProductContainer/ProductContainer.vue";
import DeskTopFooter from "./components/BaseAppShellFooter/DeskTopFooter.vue";
import LoaderFordata from "./components/ProductContainer/LoaderForData.vue"
import OurStory from "./components/ProductContainer/OurStory.vue";

export default {
  components: {
    DeskTopHeader,
    ProductContainer,
    DeskTopFooter,
    LoaderFordata,
    OurStory
  },
  data() {
    return {
      productsData: [],
      filtersData: [],
      sortingOptions: [],
      totalProductCount: 0,
      currentPagination: 1,
      totalpageNumber: 0,
      sortingValue: "",
      filterSting: "",
      gotoTop: 0,
      spinLoader: false,
      showStoryData: false
    };
  },
  methods: {
    getProductData() {
      const axios = require("axios");
      const api = `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.currentPagination}&count=20&sort_by=${this.sortingValue}&sort_dir=desc&filter=${this.sortingValue}`;
      this.spinLoader = true
      axios.get(api).then((response) => {
        console.log(response);
        this.productsData = response.data.result.products;
        this.filtersData = response.data.result.filters;
        this.sortingOptions = response.data.result.sort;
        this.totalProductCount = response.data.result.count;
        this.getTotalPageCount()
        this.spinLoader = false

      });
    },

    // Function is used to get data from api when user 
    // Change current page
    // When user applied filter
    // when user applied sorting on data
    getDataUpdateDataFromApi() {
      const axios = require("axios");
      const api = `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${this.currentPagination}&count=20&sort_by=${this.sortingValue}&sort_dir=desc&filter=${this.filterSting}`;
      this.spinLoader = true;
      axios.get(api).then((response) => {
        this.productsData = response.data.result.products;
        this.totalProductCount = response.data.result.count;
        this.getTotalPageCount()
        this.spinLoader = false;
      });
    },

    // Function is used to get current page number
    // and get data according to current page
    getProductOfCurrentPage(currentPage) {
      this.currentPagination = currentPage;
      this.getDataUpdateDataFromApi();

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
      this.getDataUpdateDataFromApi();
    },

    // Function is used check the applied filter array lenght is zero or not
    getFilters(applyFilters) {
      if (applyFilters.length) {
        if (applyFilters.length > 1) {
          let str = "";
          for (let i = 0; i < applyFilters.length; i++) {
            if (!str) {
              str = str + applyFilters[i]
            } else {
              str = str + "," + applyFilters[i]
            }
          }
          this.filterSting = str;
        } else {
          this.filterSting = applyFilters[0];
        }
        this.$router.push({ path: this.$route.fullPath, query: { filter: this.filterSting } })
        if (this.currentPagination > 1) this.currentPagination = 1;
        this.getDataUpdateDataFromApi();
      } else {
        this.filterSting = ""
        this.$router.push({ path: this.$route.fullPath, query: { filter: this.filterSting } })
        this.getDataUpdateDataFromApi();
      }
    },

    // Function is used to calculate total number of page
    getTotalPageCount() {
      this.totalpageNumber = Math.ceil(this.totalProductCount / 20)
    },
    showOurStory(bollean) {
      console.log("parent" ,bollean)
      this.showStoryData = bollean
    }

  },
  mounted() {
    this.getProductData();
  },
  watch: {
    filterSting() {
      this.getDataUpdateDataFromApi();
    }
  }
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
