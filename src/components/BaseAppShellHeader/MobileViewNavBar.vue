<template>
    <div class="side-bar-container">
        <div class="upper-header">
            <p class="text">
                COMPLIMENTARY GIFT BOX PACKING ON ALL PRE-PAID ORDERS
            </p>
        </div>

        <div class="lover-header">
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
        <div @click="hideNavBar" v-if="isShowSideNavBar" class="slide-nav-container">

            <div class="nav-container">
                <div class="login-container">
                    <div>
                        <p class="login-text">Login</p>
                    </div>
                    <div>
                        <img @click="hideNavBar" class="cross-icon" src="@/assets/whiteCrossIcon.png" alt="">
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

        </div>
    </div>
</template>

<script>
export default {
    name: "MobileViewNavBar",
    data() {
        return {
            isShowSideNavBar: false
        }
    },
    methods: {
        showNavBar() {
            this.isShowSideNavBar = true
        },
        hideNavBar() {
            this.isShowSideNavBar = false
        }
    }
};
</script>

<style scoped>
.side-bar-container {
    width: 100%;
}
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
    column-gap: 20px;
    align-items: center;
}

.action-image {
    width: 75%;
}

.slide-nav-container {
    width: 100%;
    background-color: transparent;
}

.nav-container {
    width: 75%;
    position: fixed;
    top: 0px;
    height: 100vh;
    z-index: 5453;
}
.login-container {
    background-color: #501337;
    padding: 10px 20px ;
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
