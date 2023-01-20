<template>
    <div>
        <div v-if="isShowSortingList" class="sorting-option-container">
            <div class="sorting-option">
                <ul>
                    <li>Sort: By</li>
                    <li v-for="(sortoption, index) in sortingOptions" :key="index">
                        {{ sortoption.label }}
                    </li>
                </ul>
            </div>
        </div>
        <div class="sort-filter-container">
            <div class="sort-button">
                <button @click="isShowSortingList = !isShowSortingList" class="action-button" type="button">
                    SORT: BY
                </button>
            </div>
            <div class="filter-button">
                <button class="action-button" type="button">FILTER</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Sort&FilterBar",
    props: ["sortingOptions"],
    data() {
        return {
            isShowSortingList: false,
        };
    },
};
</script>

<style scoped>
.sort-filter-container {
    width: 100%;
    background-color: #fff;
    position: fixed;
    z-index: 10000;
    bottom: 0px;
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
    padding: 18px 2px;
    border: none;
    font-weight: 800;
    cursor: pointer;
}

.sorting-option-container {
    position: fixed;
    width: 95%;
    margin: auto;
    background-color: #fff;
    bottom: 50px;
    z-index: 54553;
}
</style>
