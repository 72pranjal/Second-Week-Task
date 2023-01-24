<template>
  <div class="nav-bar-container">
    <div class="both-nav-bar">
      <!-- upper header............ -->
      <div class="upper-nav-bar">
        <div class="upper-nav-container">
          <div class="first-part">
            <p class="text">
              COMPLIMENTARY GIFT BOX PACKING ON ALL PRE-PAID ORDERS
            </p>
          </div>
          <div class="second-part">
            <ul class="nav-items">
              <li><img src="@/assets/nationalFlag.png" alt="" /></li>
              <li>OUR STORES</li>
              <li>MY ACCOUNT</li>
              <li>BLOG</li>
            </ul>
          </div>
        </div>
      </div>

      <!-- lover header........................... -->
      <div :class="[navBarFixed ? 'lower-header-container-fixed' : 'lower-header-container']">
        <div class="first">
          <ul class="first-part-items">
            <li>
              <div class="show-in-line">
                <p>WOMEN</p>
                <span>
                  <img class="down-arrao-icon" src="@/assets/downArrowImage.webp" alt="" />
                </span>
              </div>
            </li>
            <li>
              <div class="show-in-line">
                <p>MEN</p>
                <span><img class="down-arrao-icon" src="@/assets/downArrowImage.webp" alt="" /></span>
              </div>
            </li>
            <li>SALE</li>
            <li>
              <div class="show-in-line">
                <p>COLLECTION</p>
                <span>
                  <img class="down-arrao-icon" src="@/assets/downArrowImage.webp" alt="" />
                </span>
              </div>
            </li>
          </ul>
        </div>

        <div class="logo-container">
          <img src="@/assets/Group 2.png" alt="" />
        </div>

        <div class="second">
          <ul class="first-part-items">
            <li>
              <div class="show-in-line">
                <p>OUR STORY</p>
                <span>
                  <img class="down-arrao-icon" src="@/assets/downArrowImage.webp" alt="" />
                </span>
              </div>
            </li>
            <li>
              <div class="show-in-line">
                <p>CRAFTMANSHIP</p>
                <span>
                  <img class="down-arrao-icon" src="@/assets/downArrowImage.webp" alt="" />
                </span>
              </div>
            </li>
          </ul>
        </div>

        <div class="action-icon-container">
          <span>
            <img class="action-image" src="@/assets/Group 252.png" alt="" />
          </span>
        </div>
      </div>
    </div>

    <!-- mobile Nav bar ................................ -->
    <div class="mobile-nav">
      <MobileViewNavBar :navBarFixed="navBarFixed" />
    </div>

    <!-- after nav bar text................... -->
    <div class="text-container">
      <p class="middle-text">Women Pashmina Shawls</p>
      <p class="count-number">{{ totalProductCount }} Items</p>
    </div>
  </div>
</template>

<script>
import MobileViewNavBar from "./MobileViewNavBar.vue"
export default {
  name: "DeskTopHeader",
  components: {
    MobileViewNavBar,
  },
  props: ["totalProductCount", "currentPagination"],
  data() {
    return {
      scrollPosition: null,
      navBarFixed: false
    }
  },
  methods: {
    // Function is use to calculate scroll position
    getCurrentPosition() {
      this.scrollPosition = window.scrollY;
      if (this.scrollPosition > 30) {
        this.navBarFixed = true
      } else {
        this.navBarFixed = false
      }
    }
  },
  mounted() {
    window.addEventListener("scroll", this.getCurrentPosition)
  },
   watch: {
    currentPagination(newVal) {
    if(newVal > 1) window.scrollTo(100, 100)
    
    }
   }


};
</script>

<style scoped>
.mobile-nav {
  display: none;
}

.both-nav-bar {
  display: block;
}

.upper-nav-bar {
  background-color: #9d8b61;
  width: 100%;
  border-bottom: 1px solid #ccc;
}

.upper-nav-container {
  display: flex;
  justify-content: space-between;
  color: white;
  font-size: 14px;
  padding: 10px 12px;
  align-items: center;

}

.first-part {
  box-sizing: border-box;
}

.text {
  margin: 0px;
}

.second-part {
  box-sizing: border-box;
}

.nav-items {
  display: flex;
  float: right;
  align-items: center;
  column-gap: 30px;
  margin: 0px;
}

li {
  list-style: none;
  cursor: pointer;
}

/* lover nav bar ................... */
.lower-header-container {
  color: #000;
  width: 100%;
  padding: 1% 0%;
  display: flex;
  font-size: 16px;
  background-color: #fff;
  box-shadow: 0px 4px 12px 0px rgb(0 0 0 / 5%);
}

.lower-header-container-fixed {
  color: #000;
  width: 100%;
  padding: 1% 0%;
  display: flex;
  font-size: 16px;
  background-color: #fff;
  box-shadow: 0px 4px 12px 0px rgb(0 0 0 / 5%);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 2323;
}

.down-arrao-icon {
  width: 20px;
  height: 20px;
}

.first {
  width: 43%;
  box-sizing: border-box;
  margin-top: 2%;
}

.logo-container {
  width: 15%;
  box-sizing: border-box;
}

.second {
  width: 28%;
  box-sizing: border-box;
  margin-top: 2%;
}

.show-in-line {
  display: flex;
  align-items: center;
}

.action-icon-container {
  width: 10%;
  box-sizing: border-box;
  margin-top: 4.4%;
  margin-left: 1%;
  text-align: right;
}

.action-image {
  width: 80%;
}

.first-part-items {
  display: flex;
  align-items: center;
  column-gap: 25px;
}

/* <!-- after nav bar text................... --> */
.text-container {
  text-align: center;
  padding: 3% 0%;
  box-sizing: border-box;
  width: 100%;
}

.middle-text {
  font-size: 32px;
  color: #303030;
  margin: 0px;
}

.count-number {
  margin: 0px;
  color: #000;
  font-size: 18px;
  font-weight: 800;
}

/* women list open on hover ...................... */
/* .women-list-container {
  width: 100%;
  max-width: 100%;
  background-color: #fff;
}

.womens-link-list {
  flex: 0 0 100%;
  padding: 10px 20px;
  display: flex;

}

.mportant-links-container {
  display: flex;
  flex: 0 0 50%;
  justify-content: space-between;
}

.image-container {
  width: 50%;
} */


@media screen and (max-width: 999px) {
  .both-nav-bar {
    display: none;
  }

  .mobile-nav {
    display: block;
  }

  .middle-text {
    font-size: 20px;
  }

  .count-number {
    font-size: 16px;

  }
}
</style>
