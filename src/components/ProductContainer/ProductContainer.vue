<template>
  <div class="main-container">
    <!-- Contain filter hide button and sorting options......... -->
    <div class="sort-option-container">
      <!-- hide filter button........... -->
      <div class="hide-filter-container">
        <img v-if="isHideSideFilters" @click="hideSideFilter" class="hide-all-filter" src="@/assets/sideHilterHide.svg"
          alt="" />
        <button class="show-filter-button" v-else @click="showSideFilters">
          Show Filter
        </button>
      </div>
      <!-- applied filters chips........... -->
      <div class="applied-chip-container" v-if="appliedFiltersForChips.length">
        <div class="cross-icon-container" v-for="(appliedFilter, index) in appliedFiltersForChips" :key="index">
          <span class="filter-chip">
            <p class="filter-name">{{ appliedFilter }}</p>
            <span>
              <img @click="removeAppliedFilter(index)" class="cross-icon" src="@/assets/darkCrosIcon.png" alt="" />
            </span>
          </span>
        </div>
      </div>
      <!-- sorting options dropDown................. -->
      <div class="dropdown-container">
        <select v-model="selectedSortingOption" class="drop-down-box">
          <option class="drop-options" value="" disabled selected>
            Sort By
          </option>
          <option v-for="(option, index) in sortingOptions" :key="index" class="drop-options" :value="option.code">
            {{ option.label }}
          </option>
        </select>
      </div>

      <!-- mobile view botton nav bar............................. -->
      <div class="bottom-nav-bar">
        <SortAndFilterBar
         :sortingOptions="sortingOptions" 
         @showMobileFIlter="showFilters"
         />
      </div>
    </div>

    <!-- Contain side filter and product.................. -->
    <div class="filter-product-container">
      <!-- side filter bar container ........... -->
      <div v-if="isHideSideFilters" class="side-filter-container">
        <div v-if="appliedFiltersForChips.length">
          <button @click="clearAllAppliedFilters" class="clear-button">
            Clear All
          </button>
        </div>
        <div>
          <div class="filter-container" v-for="(filters, index) in containFiltersData" :key="index">
            <div class="filter-head">
              <p @click="showSubFIlters(filters.filter_lable)">
                {{ filters.filter_lable }}
              </p>
              <span v-if="!particularOpenSubFilter.includes(filters.filter_lable)">
                <img @click="showSubFIlters(filters.filter_lable)" class="plus-icon" src="@/assets/plusIcon.png"
                  alt="" />
              </span>
              <span v-else>
                <img @click="showSubFIlters(filters.filter_lable)" class="plus-icon" src="@/assets/minusIcon.png"
                  alt="" />
              </span>
            </div>
            <div v-if="particularOpenSubFilter.includes(filters.filter_lable)">
              <ul class="subfilters">
                <li v-for="(subFilter, index) in filters.options" :key="index">
                  <input class="checkbox" type="checkbox" v-model="appliedFiltersForChips"
                    @click="getAppliedFilter(subFilter)" :id="subFilter.value" :value="subFilter.value" />
                  <label :for="subFilter.value" class="lable-subfilter">{{
                    subFilter.value
                  }}</label>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <!-- all products container........... -->
      <!-- :style="{ width: isHideSideFilters ? '75%' : '100%' }" -->
      <div class="product-container">
        <div class="one-product-container">
          <div v-for="(products, index) in containProductData" :key="index" class="product-image-container">
            <div class="product-image">
              <img class="image-kurta" :src="products.image" alt="" />

              <div class="heart-image-container">
                <img class="heart-image" src="@/assets/heartImage.svg" alt="" />
              </div>
            </div>

            <div class="title-container">
              <p>
                {{
                  products.Product_Title_FH === null
                    ? products.name
                    : products.Product_Title_FH
                }}
              </p>
              <p>Rs. {{ products.price }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Side filter in mobile vue................................................. -->
    <div v-if="showingMobileFilter" class="mobile-filter-container">
      <div class="mobile-filter">
        <div class="header">
          <p class="header-text">Filters</p>
          <div v-if="appliedFiltersForChips.length">
          <button @click="clearAllAppliedFilters" class="clear-button">
            Clear All
          </button>
        </div>
        </div>
        <div v-for="(filters, index) in containFiltersData" :key="index">
          <div class="filters-container">
            <div class="filter-lable-container">
                <button 
                class="label-button"
                :style="{backgroundColor: particularOpenSubFilter.includes(filters.filter_lable) ? '#fff' : ''}"
                 @click="showSubFIltersMobileView(filters.filter_lable)"
                 >
                {{ filters.filter_lable }}
              </button>
            </div>
            <div v-if="particularOpenSubFilter.includes(filters.filter_lable)" class="filter-options-container">
              <ul class="subfilters">
                <li v-for="(subFilter, index) in filters.options" :key="index">
                  <input class="checkbox" type="checkbox" v-model="appliedFiltersForChips" @click="getAppliedFilter(subFilter)"
                    :id="subFilter.value" :value="subFilter.value" />
                  <label :for="subFilter.value" class="lable-subfilter">{{
                    subFilter.value
                  }}</label>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Pagination section.................................. -->
    <div class="pagination-container">
      <div class="total-page-container">
        <span>Page {{ currentPageNumber }} of 97 </span>
      </div>

      <div class="counting-container">
        <span class="show-in-desktop-view">
          <button class="next-button" type="button" :style="{ opacity: currentPageNumber > 1 ? '' : '0.25' }"
            @click="goToPreviousPage">
            Previous
          </button>
        </span>
        <span class="show-in-mobile-view">
          <img @click="goToPreviousPage" class="goto-icon" src="@/assets/leftarrowIcon.png" alt=""
            :style="{ opacity: currentPageNumber > 1 ? '' : '0.25' }" />
        </span>
        <button v-for="(pageCount, index) in paginationNumbers" :key="index" class="goto-clickable-page" :style="{
          backgroundColor:
            currentPageNumber === pageCount ? '#0C0C0C' : '#FFFFFF',
          color: currentPageNumber === pageCount ? 'white' : '#303030',
        }" type="button" @click="handleClickThenActive(pageCount)">
          {{ pageCount }}
        </button>
        <span class="show-in-desktop-view">
          <button class="next-button" type="button" :style="{ opacity: currentPageNumber < 97 ? '' : '0.25' }"
            @click="gotoNextPage">
            Next
          </button>
        </span>
        <span class="show-in-mobile-view">
          <img class="goto-icon" @click="gotoNextPage" src="@/assets/rightArrowIcon.png" alt=""
            :style="{ opacity: currentPageNumber < 97 ? '' : '0.25' }" />
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import SortAndFilterBar from "../BaseAppShellHeader/SortAndFilterBar.vue";

export default {
  name: "ProductContainer",
  components: {
    SortAndFilterBar,
  },
  props: [
    "dataForFilters",
    "dataForProducts",
    "dataForSorting",
    "currentPagination",
  ],
  data() {
    return {
      containFiltersData: [],
      containProductData: [],
      particularOpenSubFilter: [],
      sortingOptions: [],
      appliedFiltersForChips: [],
      isHideSideFilters: true,
      selectedSortingOption: "",
      paginationNumbers: [1, 2, 3, 4, 5, 6],
      currentPageNumber: 1,
      appliedFilter: [],
      showingMobileFilter: false,
    };
  },
  methods: {

    // Function is used for open and hide sub filters in destTop view
    showSubFIlters(productId) {
      if (!this.particularOpenSubFilter.includes(productId)) {
        this.particularOpenSubFilter.push(productId);
      } else {
        let index = this.particularOpenSubFilter.indexOf(productId);
        this.particularOpenSubFilter.splice(index, 1);
      }
    },

    // Function is used for open and hide sub filters in mobile view
    showSubFIltersMobileView(productId) {
      if (!this.particularOpenSubFilter.includes(productId)) {
        this.particularOpenSubFilter.shift()
        this.particularOpenSubFilter.push(productId);
      } else {
        this.particularOpenSubFilter.pop();
      }
    },

    // Function is used to remove applied filter in chips section when click
    // on cross icon
    removeAppliedFilter(index) {
      this.appliedFiltersForChips.splice(index, 1);
      this.appliedFilter.pop();
      this.$emit("getFilterString", this.appliedFilter);
    },

    // function is use to hideside filter
    hideSideFilter() {
      this.isHideSideFilters = false;
    },
    // function is use to show side filters filter
    showSideFilters() {
      this.isHideSideFilters = true;
    },

    // function is use to clear all applied filters
    clearAllAppliedFilters() {
      this.appliedFiltersForChips.splice(0, this.appliedFiltersForChips.length);
      this.appliedFilter.splice(0, this.appliedFilter.length);
      this.$emit("getFilterString", this.appliedFilter);
    },

    // FUnction is used to sort products by selected options from dropdown
    sortBySelectedOption() {
      this.$emit("sortData", this.selectedSortingOption);
    },

    // Function is used for pagination active button
    handleClickThenActive(pageNo) {
      if (!(this.currentPageNumber === pageNo)) {
        this.currentPageNumber = pageNo;
        this.$emit("handleClickThenActive", this.currentPageNumber);
      } else {
        this.currentPageNumber = 1;
      }
    },

    // Function is used to goto page with increment of one in
    // current page using next button
    gotoNextPage() {
      if (this.currentPageNumber < 97) {
        this.currentPageNumber += 1;
        this.$emit("handleClickThenActive", this.currentPageNumber);
      }
      if (
        this.currentPageNumber >
        this.paginationNumbers[this.paginationNumbers.length - 1]
      ) {
        this.numberWhenClickNextButton();
      }
      return;
    },

    // Function is used to goto page with decrement of one in
    // current page using previous button
    goToPreviousPage() {
      if (this.currentPageNumber > 1) {
        this.currentPageNumber -= 1;
        this.$emit("handleClickThenActive", this.currentPageNumber);
      }
      if (this.currentPageNumber < this.paginationNumbers[0]) {
        this.numberWhenClickPreButton();
      }
      return;
    },

    // Manage pagination number when click on the next button
    numberWhenClickNextButton() {
      this.paginationNumbers.splice(0, this.paginationNumbers.length);
      for (
        let i = this.currentPageNumber;
        i <= this.currentPageNumber + 5;
        i++
      ) {
        this.paginationNumbers.push(i);
        if (i >= 97) break;
      }
    },

    // Manage pagination number when click on the previous button
    numberWhenClickPreButton() {
      this.paginationNumbers.splice(0, this.paginationNumbers.length);
      for (
        let i = this.currentPageNumber - 5;
        i <= this.currentPageNumber;
        i++
      ) {
        this.paginationNumbers.push(i);
      }
    },

    // Function is used to get data  from parent component
    getDataFrom() {
      this.containFiltersData = this.dataForFilters;
      this.containProductData = this.dataForProducts;
      this.sortingOptions = this.dataForSorting;
    },

    // Function is used get applied filter and store in array then send to api
    getAppliedFilter(applyFilter) {
      let ispushed = true;
      let index = null;
      let codeAndValueWithHiphan = applyFilter.code + "-" + applyFilter.value;
      for (let i = 0; i <= this.appliedFilter.length; i++) {
        if (this.appliedFilter[i] === codeAndValueWithHiphan) {
          ispushed = false;
          index = i;
          break;
        }
      }
      if (ispushed) {
        this.appliedFilter.push(codeAndValueWithHiphan);
      } else {
        this.appliedFilter.splice(index, 1);
      }
      this.$emit("getFilterString", this.appliedFilter);
    },
    handler() {
      // Do Something
      console.log("Page reload");
    },

    // Function is use to show filter in moblie view
    showFilters(boolean) {
      this.showingMobileFilter = boolean;
    }
  },

  created() {
    window.addEventListener("beforeunload", this.handler);
  },
  mounted() {
    this.getDataFrom();
  },
  watch: {
    selectedSortingOption() {
      this.sortBySelectedOption();
    },
    dataForProducts() {
      this.getDataFrom();
    },
    currentPagination() {
      this.currentPageNumber = this.currentPagination;
    },
  },
};
</script>

<style scoped>
.sort-option-container {
  width: 100%;
  height: auto;
  display: flex;
  margin: 20px 0px;
  align-items: center;
  justify-content: space-between;
}

.hide-filter-container {
  width: 20%;
  margin: 10px 3px;
  display: block;
}

.applied-chip-container {
  width: 58%;
  height: auto;
  display: flex;
  flex-wrap: wrap;
  column-gap: 10px;
  row-gap: 10px;
}

.filter-chip {
  display: flex;
  column-gap: 10px;
  align-items: center;
}

.dropdown-container {
  width: 15%;
  margin: 10px;
  display: block;
}

.hide-all-filter {
  width: 44%;
  cursor: pointer;
}

.show-filter-button {
  padding: 12px;
  font-size: 16px;
  color: #303030;
  cursor: pointer;
  background-color: #ffffff;
}

.cross-icon-container {
  font-size: 13px;
  padding: 2px 24px;
  border-radius: 18px;
  border: 1px solid #707070;
  display: inline-block;
}

.filter-name {
  white-space: pre;
}

.cross-icon {
  width: 10px;
  height: 10px;
  cursor: pointer;
}

.drop-down-box {
  width: 100%;
  height: 40px;
  padding: 4px;
  font-size: 16px;
  border: 1px solid #707070;
  cursor: pointer;
}

.drop-options {
  cursor: pointer;
  font-size: 16px;
}

/* filter and product place style...................... */
.mobile-filter-container {
  display: none;
}

.filter-product-container {
  width: 100%;
  display: flex;
  column-gap: 20px;
}

.filter-container {
  border-bottom: 1px solid #707070;
  /* padding: 30px; */
}

.side-filter-container {
  flex: 0 0 22%;
  height: auto;
  box-sizing: border-box;
  background-color: #ffffff;
  font-size: 16px;
  display: block;
}

li {
  list-style: none;
  color: #303030;
  cursor: pointer;
}

.clear-button {
  padding: 5px 12px;
  font-size: 15px;
  color: #000;
  cursor: pointer;
  border-radius: 50px;
  border: 1px solid #707070;
  background-color: #fff;
}

.clear-button:hover {
  background-color: #000;
  color: #fff;
}

.subfilters {
  margin: 0px;
  padding: 0px;
}

.filter-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px 0px;
}

.plus-icon {
  height: 20px;
  width: 20px;
  cursor: pointer;
  align-items: center;
}

.checkbox {
  height: 18px;
  width: 18px;
  margin: 8px;
  cursor: pointer;
  background-color: black;
}

/* style for product data................................ */
.product-container {
  width: 75%;
  box-sizing: border-box;
}

.product-image {
  position: relative;
}

.product-image-container {
  width: 24%;
}

.image-kurta {
  width: 100%;
}

.one-product-container {
  display: flex;
  row-gap: 20px;
  column-gap: 10px;
  flex-wrap: wrap;
}

.heart-image-container {
  position: absolute;
  top: 10px;
  right: 5px;
}

.heart-image {
  width: 27px;
}

/* pagination section ............................... */
.pagination-container {
  width: 100%;
  border-top: 1px solid black;
  margin: 30px 0px;
  padding: 30px 0px;
  display: flex;
}

.total-page-container {
  width: 15%;
}

.counting-container {
  width: 80%;
  margin-left: 10px;
  display: flex;
  column-gap: 20px;
  align-items: center;
  font-size: 16px;
  color: #4c0b36;
  text-align: center;
}

.goto-clickable-page {
  padding: 10px;
  margin: 0px 6px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

.next-button {
  padding: 10px;
  color: #4c0b36;
  font-size: 16px;
  background-color: #ffffff;
  border: none;
  cursor: pointer;
}

.next-button:hover {
  color: white;
  background-color: black;
}

.bottom-nav-bar {
  display: none;
}

.show-in-desktop-view {
  display: block;
}

.show-in-mobile-view {
  display: none;
}

@media screen and (max-width: 768px) {
  .side-filter-container {
    display: none;
  }

  .product-container {
    width: 100%;
    box-sizing: border-box;
  }

  .product-image-container {
    width: 48%;
  }

  .image-kurta {
    width: 100%;
  }

  .one-product-container {
    justify-content: space-between;
    display: flex;
  }

  .hide-filter-container {
    display: none;
  }

  .dropdown-container {
    display: none;
  }

  .bottom-nav-bar {
    display: block;
  }

  .show-in-desktop-view {
    display: none;
  }

  .show-in-mobile-view {
    display: block;
  }

  .goto-icon {
    width: 16px;
    height: 16px;
  }

  /* Style for filter in mobile view................................................ */
  .mobile-filter-container {
    display: block;
    width: 100%;
    position: fixed;
    top: 0px;
    left: 0px;
    right: 0px;
    z-index: 3242;
    background-color: #fff;
  }

  /* .mobile-filter {
    padding: 5px 2px;
  } */
  .header {
    flex: 0 0 100%;
    padding: 0px 20px;
    background-color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 5px;
    border-bottom: 1px solid #ccc;
  }
  .header-text {
    font-size: 18px;
    font-weight: 600;
    padding: 15px 10px;
    color: #000;
  }
  .filters-container {
    width: 100%;
    display: flex;
    align-items: center;
  }
  .filter-lable-container {
    width: 25%;
  }
  .label-button {
    width: 100%;
    border: none;
    padding: 10px;
  }
  .filter-options-container {
    width: 70%;
  }
}

@media only screen and (max-width: 1024px) and (min-width: 769px) {
  .product-image-container {
  width: 32%;
}
} 
</style>
