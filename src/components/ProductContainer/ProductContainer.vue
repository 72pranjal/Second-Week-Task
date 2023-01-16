<template>
  <div class="main-container">
    <!-- Contain filter hide button and sorting options......... -->
    <div class="sort-option-container">
      <!-- hide filter button........... -->
      <div class="hide-filter-container">
        <img
          v-if="isHideSideFilters"
          @click="hideSideFilter"
          class="hide-all-filter"
          src="@/assets/sideHilterHide.svg"
          alt=""
        />
        <button class="show-filter-button" v-else @click="showSideFilters">
          Show Filter
        </button>
      </div>
      <!-- applied filters chips........... -->
      <div class="applied-chip-container" v-if="appliedFilters.length">
        <div class="filter-chip">
          <span
            class="cross-icon-container"
            v-for="(appliedFilter, index) in appliedFilters"
            :key="index"
          >
            <p class="filter-name">{{ appliedFilter }}</p>
            <span>
              <img
                @click="removeAppliedFilter(index)"
                class="cross-icon"
                src="@/assets/crossIcon.png"
                alt=""
              />
            </span>
          </span>
        </div>
      </div>
      <!-- sorting options dropDown................. -->
      <div class="dropdown-container">
        <select v-model="selectedSortingOption" class="drop-down-box">
          <option class="drop-options" value="" disabled selected>Sort By</option>
          <option
            v-for="(option, index) in sortingOptions"
            :key="index"
            class="drop-options"
            :value="option.code"
          >
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
          <div
            class="filter-container"
            v-for="(filters, index) in containFiltersData"
            :key="index"
          >
            <div class="filter-head">
              <p>{{ filters.filter_lable }}</p>
              <span
                v-if="!particularOpenSubFilter.includes(filters.filter_lable)"
              >
                <img
                  @click="showSubFIlters(filters.filter_lable)"
                  class="plus-icon"
                  src="@/assets/plusIcon.png"
                  alt=""
                />
              </span>
              <span v-else>
                <img
                  @click="showSubFIlters(filters.filter_lable)"
                  class="plus-icon"
                  src="@/assets/minusIcon.png"
                  alt=""
                />
              </span>
            </div>
            <div v-if="particularOpenSubFilter.includes(filters.filter_lable)">
              <ul class="subfilters">
                <li v-for="(subFilter, index) in filters.options" :key="index">
                  <input
                    class="checkbox"
                    type="checkbox"
                    v-model="appliedFilters"
                    :id="subFilter.value"
                    :value="subFilter.value"
                  />
                  <label :for="subFilter.value" class="lable-subfilter">{{
                    subFilter.value
                  }}</label>
                  <!-- <span>({{ subFilter.total }})</span> -->
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <!-- all products container........... -->
      <div class="product-container">
        <div class="image-container">
          <div
            class="one-product"
            v-for="(products, index) in containProductData"
            :key="index"
          >
            <div class="product-image-container">
              <img class="product-image" :src="products.image" alt="" />
              <div class="heart-image-container">
                <img class="heart-image" src="@/assets/heartImage.svg" alt="" />
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
    </div>

    <!-- Pagination section.................................. -->
    <div class="pagination-container">

      <div class="total-page-container">
             
      </div>
      
      <div class="counting-container">

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductContainer",
  props: ["dataForFilters", "dataForProducts", "dataForSorting"],
  data() {
    return {
      containFiltersData: [],
      containProductData: [],
      particularOpenSubFilter: [],
      sortingOptions: [],
      appliedFilters: [],
      isHideSideFilters: true,
      selectedSortingOption: "",
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
    sortBySelectedOption(selectedVal) {
      if (selectedVal === "price") {
        this.containProductData.sort(function(product1, product2){
          return (product1.price - product2.price)
        });
      } else if (selectedVal === "discount") {
        this.containProductData.sort(function(product1, product2){
           return (product1.discount - product2.discount)
        });
      } else if (selectedVal === "product_position") {
        this.containProductData.sort(function(product1, product2){
          return (product1.product_position - product2.product_position)
        });
      } else {
        return;
      }
    },
  },
  mounted() {
    this.containFiltersData = this.dataForFilters;
    this.containProductData = this.dataForProducts;
    this.sortingOptions = this.dataForSorting;
  },
  watch: {
    selectedSortingOption(newVale) {
      this.sortBySelectedOption(newVale);
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
  margin: 2%;
}
.applied-chip-container {
  width: 58%;
}
.filter-chip {
  display: flex;
  column-gap: 2%;
  height: 40px;
}
.dropdown-container {
  width: 15%;
  margin: 1%;
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
  padding: 20px;
  align-items: center;
  border-radius: 20px;
  border: 1px solid black;
  box-sizing: border-box;
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
}
.filter-container {
  border-bottom: 1px solid #707070;
  padding: 3%;
}
.side-filter-container {
  width: 22%;
  height: auto;
  box-sizing: border-box;
  padding: 2%;
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
}
.plus-icon {
  height: 20px;
  width: 20px;
  align-items: center;
}
.checkbox {
  height: 18px;
  width: 18px;
  margin: 4%;
  cursor: pointer;
  background-color: black;
}

/* style for product data................................ */
.product-container {
  width: 75%;
  box-sizing: border-box;
}
.image-container {
  display: flex;
  column-gap: 22px;
  row-gap: 10px;
  flex-wrap: wrap;
}
/* .product-image {
  width: 250px;
  height: auto;
} */
.product-image-container {
  position: relative;
}
.heart-image-container {
  position: absolute;
  /* position: fixed; */
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
  margin: 3% 0%;
}
</style>
