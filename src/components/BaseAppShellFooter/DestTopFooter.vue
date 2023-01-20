<template>
  <div class="footer-container">
    <!-- footer head........................... -->
    <div class="head-line-container">
      <img class="head-line" src="@/assets/footerHeadLine.svg" alt="" />
      <div class="image-container">
        <img class="footer-image" src="@/assets/footerImage.svg" alt="" />
      </div>
    </div>

    <!-- footer in desktop view body.................................. -->
    <div class="footer">
      <div class="footer-body-container">
        <div class="footer-link-container">
          <ul class="links">
            <li class="heading">SHOP</li>
            <li>Men</li>
            <li>Women</li>
            <li>Home</li>
            <li>Sale</li>
            <li>Collection</li>
          </ul>
          <ul class="links">
            <li class="heading">QUICK LINKS</li>
            <li>Ahujasons Export</li>
            <li>Our Story</li>
            <li>Lageacy</li>
            <li>Craftman</li>
            <li>Blogs</li>
          </ul>
          <ul class="links">
            <li class="heading">CUSTOM SERVICES</li>
            <li>Tersm & Conditions</li>
            <li>Shipping & Delivery</li>
            <li>Returns & Collection</li>
            <li>Contact Us</li>
            <li>Store Oppoinment</li>
          </ul>
          <ul class="links">
            <li class="heading">MY PROFILE</li>
            <li>My Acount</li>
            <li>Track Order</li>
            <li>My Cart</li>
            <li>Wishlist</li>
            <li>Order History</li>
          </ul>
        </div>
        <div class="footer-social-media-container">
          <div class="email-subscribe-container">
            <p>SIGN UP AND SAVE</p>
            <p>
              Subscribe to our newsletter and get 10% off your first purchase
            </p>
            <div class="input-button-container">
              <input
                class="input-filed"
                type="text"
                placeholder="Enter your email address"
              />
              <button class="subscribe-button">Subscibe</button>
            </div>
          </div>
          <div class="social-meadia-container">
            <p>GIVE US A FOLLOW</p>
            <div class="social-meadia-images">
              <img src="@/assets/facebook.svg" alt="" />
              <img src="@/assets/twiter.svg" alt="" />
              <img src="@/assets/linkdin.svg" alt="" />
              <img src="@/assets/pather.svg" alt="" />
              <img src="@/assets/youtube.svg" alt="" />
            </div>
          </div>

          <div class="copyright-link">
            <p>Copyright © 2021 by Ahujasons I Powered by GreenHonchos</p>
          </div>
        </div>
      </div>
    </div>

    <!-- footer in mobile view....................................... -->
    <div class="mobile-footer-container">
      <div class="mobile-footer">
        <div class="social-meadia-container">
          <p class="text">GIVE US A FOLLOW</p>
          <div class="social-meadia-images">
            <ul class="social-meadia">
              <li><img src="@/assets/facebook.svg" alt="" /></li>
              <li><img src="@/assets/twiter.svg" alt="" /></li>
              <li><img src="@/assets/linkdin.svg" alt="" /></li>
              <li><img src="@/assets/pather.svg" alt="" /></li>
              <li><img src="@/assets/youtube.svg" alt="" /></li>
            </ul>
          </div>
        </div>
        <div class="input-field-container">
          <p class="text1">Subscribe to our newsletter</p>
          <div class="input-button-container">
            <input
              class="input-filed"
              type="text"
              placeholder="Enter your email address"
            />
            <button class="subscribe-button">Subscibe</button>
          </div>
        </div>

        <div class="mobile-links-container">
          <ul v-for="(linkItems, index) in linksItems" :key="index">
            <div class="heading-plus-icon-container">
              <div class="heading-plus-icon">
                <li class="main-link">{{ linkItems.heading }}</li>
                <span v-if="!openedSubLink.includes(linkItems.heading)">
                  <img
                    @click="showSubList(linkItems.heading)"
                    class="action-icon"
                    src="@/assets/plusIcon.png"
                    alt=""
                  />
                </span>
                <span v-else>
                  <img
                    @click="showSubList(linkItems.heading)"
                    class="action-icon"
                    src="@/assets/minusIcon.png"
                    alt=""
                  />
                </span>
              </div>

              <ul v-if="openedSubLink.includes(linkItems.heading)">
                <li v-for="(link, index) in linkItems.sublinks" :key="index">
                  {{ link }}
                </li>
              </ul>
            </div>
          </ul>
        </div>

        <div class="copyright-link">
          <p class="copyright-text">
            Copyright © 2021 by Ahujasons I Powered by GreenHonchos
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DestTopFooter",
  data() {
    return {
      linksItems: [
        {
          heading: "SHOP",
          sublinks: ["Men", "Women", "Sale", "Collection"],
        },
        {
          heading: "QUICK LINKS",
          sublinks: ["Ahujasons Our Story", "Lageacy", "Craftman", "Croft"],
        },
        {
          heading: "CUSTOM SERVICES",
          sublinks: [
            "Tersm & Conditions",
            "Shipping & Delivery",
            "Returns & Collection",
            "Contact Us",
            "Store Oppoinment",
          ],
        },
        {
          heading: "MY PROFILE",
          sublinks: [
            "My Acount",
            "Track Order",
            "My Cart",
            "Wishlist",
            "Order History",
          ],
        },
      ],
      openedSubLink: [],
    };
  },
  methods: {
    // Functiion is used to show sublinks in footer
    showSubList(headLink) {
      if (!this.openedSubLink.includes(headLink)) {
        this.openedSubLink.push(headLink);
      } else {
        let index = this.openedSubLink.indexOf(headLink);
        this.openedSubLink.splice(index, 1);
      }
    },
  },
};
</script>

<style scoped>
/* Footer head logo stlye.................... */
.head-line-container {
  width: 100%;
  position: relative;
  text-align: center;
  background-color: #fff;
  height: 80px;
}

.head-line {
  width: 100%;
}

.image-container {
  position: absolute;
  left: 50%;
  right: 50%;
  width: 100px;
  background-color: #fff;
  transform: translate(-50%, -50%);
}

.footer-image {
  width: 70%;
}

/* footer body style................................................. */
li {
  list-style: none;
  line-height: 40px;
  font-size: 14px;
  cursor: pointer;
}

li:hover {
  color: black;
}

ul {
  margin: 0px;
  padding: 0px;
}

.footer {
  width: 100%;
  display: block;
  background-color: #fff;
}

.mobile-footer-container {
  display: none;
}

.footer-body-container {
  padding: 10px 60px;
  display: flex;
  justify-content: space-between;
}

.footer-link-container {
  flex: 0 0 62%;
  padding: 9px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.heading {
  color: #303030;
  font-size: 16px;
  font-weight: 500;
}

.footer-social-media-container {
  width: 35%;
}

.input-button-container {
  width: 100%;
}

.input-filed {
  border: none;
  border-bottom: 1px solid #000;
  height: 40px;
  line-height: 40px;
  /* padding: 0px 80px 0px 0px; */
  color: #424242;
  font-size: 14px;
  background-color: transparent;
  border-radius: 0px;
}

input:focus {
  outline: none;
  position: relative;
  border-bottom: 1px solid #000;
  /* border-bottom: 1px solid #000; */
}

.subscribe-button {
  border: none;
  position: absolute;
  right: 12%;
  background-color: transparent;
  color: #000;
}

.social-meadia-images {
  display: flex;
  justify-content: space-between;
}

.social-meadia-container {
  margin: 40px 2px;
}

/* footer style in mobile view......................... */
@media screen and (max-width: 768px) {
  .social-meadia-container {
    margin: 4px 2px;
  }

  .footer {
    display: none;
  }

  .mobile-footer-container {
    display: block;
  }

  .mobile-footer-container {
    width: 100%;
    display: block;
    background-color: #fff;
  }

  .mobile-footer {
    padding: 40px 10px;
  }

  .text {
    font-size: 20px;
    color: #000;
    font-weight: 800;
  }

  .social-meadia {
    display: flex;
    column-gap: 30px;
  }

  .text1 {
    font-size: 18px;
    font-weight: 500;
    color: #000;
  }

  .input-field-container {
    padding-bottom: 20px;
  }

  .input-filed {
    border: none;
    border-bottom: 1px solid #000;
    height: 40px;
    line-height: 40px;
    color: #424242;
    font-size: 14px;
    width: 95%;
    background-color: transparent;
  }

  .subscribe-button {
    border: none;
    background-color: #fff;
    color: #000;
  }

  .action-icon {
    width: 20px;
    height: 20px;
  }

  .heading-plus-icon {
    display: flex;
    justify-content: space-between;
  }
  .heading-plus-icon-container {
    border-bottom: 1px solid #ccc;
    padding: 6px 0px;
    align-items: center;
  }

  .main-link {
    font-size: 16px;
    color: #000;
    font-weight: 400;
  }

  .copyright-link {
    padding: 15px 0px;
  }

  .copyright-text {
    font-size: 17px;
    color: #000;
  }
}
</style>
