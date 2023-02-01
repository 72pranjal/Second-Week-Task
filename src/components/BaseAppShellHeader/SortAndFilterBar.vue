<template>
    <div>
        <div v-if="isShowSortingList && !isShowMobileFiler" class="sorting-option-container">
            <div class="sorting-option">
                <ul>
                    <li>Sort: By</li>
                    <li 
                    v-for="(sortoption, index) in sortingOptions"
                    @click="getOptionValue(sortoption.code)"
                     :key="index"
                     >
                        {{ sortoption.label }}
                    </li>
                </ul>
            </div>
        </div>
        <div class="sort-filter-container">
            <div class="sort-button">
                <button v-if="!isShowMobileFiler" @click="isShowSortingList = !isShowSortingList" class="action-button" type="button">
                    SORT: BY
                </button>
                <button @click="hideMobileFilter" v-else type="button"  class="action-button">
                   CLOSE
                </button>
            </div>
            <div class="filter-button">
                <button v-if="appliedFilterLength === 0 " @click="showMobileFIlter" class="action-button" type="button">FILTER</button>
                <button v-else @click="hideMobileFilter" class="action-button" type="button">Apply</button>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "SortAndFilterBar",
    props: ["sortingOptions", "appliedFilterLength"],
    data() {
        return {
            isShowSortingList: false,
            isShowMobileFiler: false,
            isHideMobileFIlter: false,
        };
    },
    methods: {
        // Function is used to show filters in mobile view
        showMobileFIlter() {
            this.isShowMobileFiler = true;
            this.isShowSortingList = false
            this.$emit("showMobileFIlter", this.isShowMobileFiler)
        },
        // Function is used to hide filters in mobile view
        hideMobileFilter() {
           this.isShowMobileFiler = false
            this.$emit("showMobileFIlter", this.isShowMobileFiler)
        },
        // Function is used to get the value of selected sorting options
        getOptionValue(option) {
            this.$emit("getSelectedSort", option)
            this.isShowSortingList = false
        }
    }
};
</script>

<style scoped>
.sort-filter-container {
    width: 100%;
    max-width: 100%;
    background-color: #fff;
    position: fixed;
    z-index: 10000;
    bottom: 0px;
    left: 0px;
    right: 0px;
    display: flex;
    justify-content: space-between;
}

.sort-button {
    width: 49%;
}

.filter-button {
    width: 49%;
}

li {
    list-style: none;
    text-align: center;
    color: #000;
    padding: 14px 0px;
    margin: 0px;
    font-size: 18px;
    font-weight: 800;
    cursor: pointer;
    border-bottom: 1px solid #ccc;
}

ul {
    padding: 0px;
    margin: 0px;
}

.action-button {
    width: 100%;
    background-color: #fff;
    color: #000;
    padding: 20px 2px;
    border: none;
    font-size: 16px;
    font-weight: 800;
    cursor: pointer;
}

.sorting-option-container {
    position: fixed;
    width: 95%;
    margin: auto;
    background-color: #fff;
    bottom: 50px;
    left: 0px;
    right: 0px;
    z-index: 54553;
}
</style>
