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
      <div class="applied-chip-container" v-if="appliedFilters.length">
        <div class="filter-chip">
          <span class="cross-icon-container" v-for="(appliedFilter, index) in appliedFilters" :key="index">
            <p class="filter-name">{{ appliedFilter }}</p>
            <span>
              <img @click="removeAppliedFilter(index)" class="cross-icon" src="@/assets/crossIcon.png" alt="" />
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
    </div>

    <!-- Contain side filter and product.................. -->
    <div class="filter-product-container">
      <!-- side filter bar container ........... -->
      <div v-if="isHideSideFilters" class="side-filter-container">
        <div>
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
                  <input class="checkbox" type="checkbox" v-model="appliedFilters" :id="subFilter.value"
                    :value="subFilter.value" />
                  <label :for="subFilter.value" class="lable-subfilter">{{
                    filters.filter_lable + "_" + subFilter.value
                  }}</label>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <!-- all products container........... -->
      <div class="product-container" :style="{ width: isHideSideFilters ? '75%' : '100%' }">
        <div class="one-product-container">
          <div v-for="(products, index) in containProductData" :key="index" class=" product-image-container">
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

    <!-- Pagination section.................................. -->
    <div class="pagination-container">
      <div class="total-page-container">
        <span>Page {{ activeButton }} of 97 </span>
      </div>

      <div class="counting-container">
        <button v-for="(pageCount, index) in totalPage" :key="index" class="goto-clickable-page" :style="{
          backgroundColor: activeButton === pageCount ? '#0C0C0C' : '#FFFFFF',
          color: activeButton === pageCount ? 'white' : '#303030',
        }" type="button" @click="handleClickThenActive(pageCount)">
          {{ pageCount }}
        </button>
        <span>
          <button class="next-button" type="button" @click="gotoNextPage">
            Next
          </button>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductContainer",
  props: ["dataForFilters", "dataForProducts", "dataForSorting", "currentPagination"],
  data() {
    return {
      containFiltersData: [],
      containProductData: [],
      particularOpenSubFilter: [],
      sortingOptions: [],
      appliedFilters: [],
      isHideSideFilters: true,
      selectedSortingOption: "",
      totalPage: [1, 2, 3, 4, 5, 6],
      activeButton: 1,
    };
  },
  methods: {
    // Function is used for open and hide sub filters
    showSubFIlters(productId) {
      if (!this.particularOpenSubFilter.includes(productId)) {
        this.particularOpenSubFilter.push(productId);
      } else {
        let index = this.particularOpenSubFilter.indexOf(productId);
        this.particularOpenSubFilter.splice(index, 1);
      }
    },

    // Function is used to remove applied filter in chips section when click
    // on cross icon
    removeAppliedFilter(index) {
      this.appliedFilters.splice(index, 1);
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
      this.appliedFilters.splice(0, this.appliedFilters.length);
    },

    // FUnction is used to sort products by selected options from dropdown
    sortBySelectedOption() {
      this.$emit('sortData', this.selectedSortingOption)
    },

    // Function is used for pagination active button
    handleClickThenActive(pageNo) {
      if (!(this.activeButton === pageNo)) {
        this.activeButton = pageNo;
        this.$emit('handleClickThenActive', this.activeButton)
      } else {
        this.activeButton = 1;
      }
    },

    // Function is used to goto page with increment of one in 
    // current page using next button
    gotoNextPage() {
      if (this.activeButton < 97) {
        this.activeButton += 1;
        this.$emit('handleClickThenActive', this.activeButton)
      }
      return;
    },

    // Function is used to get data  from parent component
    getDataFrom() {
      this.containFiltersData = this.dataForFilters;
      this.containProductData = this.dataForProducts;
      this.sortingOptions = this.dataForSorting;
    }
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
      this.activeButton = this.currentPagination
    },
  },
};
</script>

<style scoped>
.sort-option-container {
  width: 100%;
  height: auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.hide-filter-container {
  width: 20%;
  margin: 20px;
}

.applied-chip-container {
  width: 58%;
  height: auto;
}

.filter-chip {
  display: flex;
  flex-wrap: wrap;
  column-gap: 10px;
  height: 35px;
}

.dropdown-container {
  width: 15%;
  margin: 10px;
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
  display: flex;
  width: auto;
  column-gap: 10px;
  padding: 0px 10px;
  align-items: center;
  border-radius: 30px;
  border: 1px solid black;
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
  cursor: pointer;
}

.drop-options {
  cursor: pointer;
  font-size: 16px;
}

/* filter and product place style...................... */
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
  padding: 20px;
  background-color: #ffffff;
  font-size: 16px;
}

li {
  list-style: none;
  color: #303030;
}

.clear-button {
  padding: 4px;
  font-size: 12px;
  color: #303030;
  cursor: pointer;
  background-color: #ffffff;
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
  column-gap: 12px;
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
  font-size: 16px;
  color: #4C0B36;
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
  color: #4C0B36;
  font-size: 16px;
  background-color: #ffffff;
  border: 1px solid #0c0c0c;
  cursor: pointer;
}
</style>
