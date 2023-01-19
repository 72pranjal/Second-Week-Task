<template>
  <div class="nav-bar-container">
   <div class="both-nav-bar">
     <!-- upper header............ -->
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

    <!-- lover header........................... -->
    <div class="lower-header-container">
      <div class="first">
        <ul class="first-part-items">
          <li>
            <div class="show-in-line">
              <p>WOMEN</p>
              <span>
                <img
                  class="down-arrao-icon"
                  src="@/assets/downArrowImage.webp"
                  alt=""
                />
              </span>
            </div>
          </li>
          <li>
            <div class="show-in-line">
              <p>MEN</p>
              <span
                ><img
                  class="down-arrao-icon"
                  src="@/assets/downArrowImage.webp"
                  alt=""
              /></span>
            </div>
          </li>
          <li>SALE</li>
          <li>
            <div class="show-in-line">
              <p>COLLECTION</p>
              <span>
                <img
                  class="down-arrao-icon"
                  src="@/assets/downArrowImage.webp"
                  alt=""
                />
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
                <img
                  class="down-arrao-icon"
                  src="@/assets/downArrowImage.webp"
                  alt=""
                />
              </span>
            </div>
          </li>
          <li>
            <div class="show-in-line">
              <p>CRAFTMANSHIP</p>
              <span>
                <img
                  class="down-arrao-icon"
                  src="@/assets/downArrowImage.webp"
                  alt=""
                />
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

    <!-- after nav bar text................... -->
    <div class="text-container">
      <p class="middle-text">Women Pashmina Shawls</p>
      <p class="count-number">{{ totalProductCount }} Items</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "DeskTopHeader",
  props: ["totalProductCount"],
};
</script>

<style scoped>
/* .both-nav-bar {
  position: fixed;
  z-index: 44444;
  background-color: cadetblue;
} */
.upper-nav-container {
  width: 100%;
  background-color: #ffffff;
  box-shadow: 1px 3px rgb(128, 128, 128);
  display: flex;
  color: #303030;
  font-size: 14px;
}
.first-part {
  width: 50%;
  box-sizing: border-box;
  padding-left: 1%;
}
.text {
  margin: 0px;
}
.second-part {
  width: 50%;
  box-sizing: border-box;
  padding-right: 1%;
}
.nav-items {
  display: flex;
  float: right;
  column-gap: 30px;
  margin: 0px;
}

li {
  list-style: none;
}
/* lover nav bar ................... */
.lower-header-container {
  color: #303030;
  width: 100%;
  padding: 1% 0%;
  display: flex;
  font-size: 16px;
  box-shadow: 1px 3px rgb(128, 128, 128);
  border-bottom-width: 20px;
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
  color: #303030;
  font-size: 18px;
}
</style>
