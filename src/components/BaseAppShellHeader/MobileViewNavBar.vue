<template>
    <div class="side-bar-container">
        <div class="upper-header">
            <p class="text">
                COMPLIMENTARY GIFT BOX PACKING ON ALL PRE-PAID ORDERS
            </p>
        </div>

        <div :class="[navBarFixed ? 'lover-header-fixed' : 'lover-header']">
            <div class="logo-container">
                <div>
                    <img class="side-nav-icon" @click="showNavBar" src="@/assets/sideNavIcon-.png" alt="" />
                </div>
                <div>
                    <img class="logo-image" src="@/assets/footerImage.svg" alt="" />
                </div>
            </div>
            <div class="action-container">
                <div>
                    <img src="@/assets/nationalFlag.png" alt="" />
                </div>
                <div>
                    <img class="action-image" src="@/assets/Group 252.png" alt="" />
                </div>
            </div>
        </div>

        <!-- slide nav bar............................... -->
        <div class="show-two-div" >
            <div v-if="isShowSideNavBar" :style="{ width: isShowSideNavBar ? '75%' : '0%' }" class="nav-container">
                <div class="login-container">
                    <div>
                        <p class="login-text">Login</p>
                    </div>
                    <div>
                        <img @click="isShowSideNavBar = !isShowSideNavBar" class="cross-icon" src="@/assets/whiteCrossIcon.png" alt="">
                    </div>
                </div>
                <div class="links-container">
                    <div class="links">
                        <p>WOMEN</p>
                        <img class="down-arrow" src="@/assets/downArrowIcon.webp" alt="">
                    </div>
                    <div class="links">
                        <p>MEN</p>
                        <img class="down-arrow" src="@/assets/downArrowIcon.webp" alt="">
                    </div>
                    <div class="links">
                        <p>Sale</p>
                    </div>
                    <div class="links">
                        <p>COLLECTION</p>
                        <img class="down-arrow" src="@/assets/downArrowIcon.webp" alt="">
                    </div>
                    <div class="links">
                        <p>OUR STORY</p>
                        <img class="down-arrow" src="@/assets/downArrowIcon.webp" alt="">
                    </div>
                    <div class="links">
                        <p>CRAFTMANSHIP</p>
                        <img class="down-arrow" src="@/assets/downArrowIcon.webp" alt="">
                    </div>

                </div>
            </div>
            <div class="close-side-nav-bar" @click="isShowSideNavBar = !isShowSideNavBar">

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "MobileViewNavBar",
    props: ["navBarFixed"],
    data() {
        return {
            isShowSideNavBar: false,
        }
    },
    methods: {
        showNavBar() {
            this.isShowSideNavBar = true
        },
    }
};
</script>

<style scoped>
.upper-header {
    background-color: #9d8b61;
    color: white;
    text-align: center;
    padding: 3px 30px;
    font-size: 14px;
}

.lover-header {
    background-color: #fff;
    padding: 10px 8px;
    display: flex;
    justify-content: space-between;
    box-shadow: 0px 4px 12px 0px rgb(0 0 0 / 5%);
}

.lover-header-fixed {
    background-color: #fff;
    padding: 10px 8px;
    display: flex;
    justify-content: space-between;
    box-shadow: 0px 4px 12px 0px rgb(0 0 0 / 5%);
    position: fixed;
    left: 0px;
    right: 0px;
    top: 0px;
    z-index: 234;
}

.logo-container {
    align-items: center;
    display: flex;
    column-gap: 10px;
}

.side-nav-icon {
    height: 25px;
    width: 25px;
}

.logo-image {
    width: 75%;
}

.action-container {
    display: flex;
    align-items: center;
    text-align: end;
}

.action-image {
    width: 75%;
}
.show-two-div {
    width: 100%;
    max-width: 100%;
    flex: 0 0 100%;
    display: flex;
    position: fixed;
    top: 0px;
    transition: 0.5s all;
    z-index: 5453;
}
.nav-container {
    width: 75%;
}
.close-side-nav-bar {
    width: 26%;
    max-width: 25%;
    background-color: rgb(0,0,0, .8);
}
.login-container {
    background-color: #501337;
    padding: 10px 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.cross-icon {
    width: 20px;
    height: 20px;
}

.login-text {
    font-size: 18px;
    color: #fff;
}

.links-container {
    background-color: #fff;
    padding: 12px 20px;
    height: 100vh;
}

.links {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 4px 0px;
    border-bottom: 1px solid #ccc;
}

.down-arrow {
    width: 25px;
    height: 25px;
}
</style>
