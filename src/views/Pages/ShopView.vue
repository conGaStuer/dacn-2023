<template>
  <Navbar />
  <div class="direct">
    <router-link to="/">Home</router-link> <span>></span>
    <router-link to="/shop" :style="{ color: '#f03333' }">Shop</router-link>
  </div>
  <div class="banner"></div>
  <div class="category">
    <div class="category-item">
      <div class="cate-item__image"></div>
      <div class="cate-item__info">
        <p>Accessories</p>
        <div class="info-text">
          <h5>Pen</h5>
          <h5>Keyboard</h5>
          <h5>Something else...</h5>
        </div>
        <button>
          Viewmore <i class="fa-solid fa-circle-chevron-right"></i>
        </button>
      </div>
    </div>
    <div class="category-item">
      <div class="cate-item__image cate-item__image1"></div>
      <div class="cate-item__info">
        <p>Ipad</p>
        <div class="info-text">
          <h5>Ipad pro</h5>
          <h5>Ipad ++</h5>
          <h5>Something else...</h5>
        </div>
        <button>
          Viewmore <i class="fa-solid fa-circle-chevron-right"></i>
        </button>
      </div>
    </div>
    <div class="category-item">
      <div class="cate-item__image cate-item__image2"></div>
      <div class="cate-item__info">
        <p>Phone</p>
        <div class="info-text">
          <h5>Xiaomi</h5>
          <h5>Redmi</h5>
          <h5>Something else...</h5>
        </div>
        <button>
          Viewmore <i class="fa-solid fa-circle-chevron-right"></i>
        </button>
      </div>
    </div>
  </div>
  <div class="products">
    <div class="filt-side">
      <div class="filter-text"><span>Filer Result</span></div>
      <div class="filter-product">
        <div class="filter-product__item">
          <button>x</button>
          <span>Ipad</span>
        </div>
        <div class="filter-product__item">
          <button>x</button>
          <span>Phone</span>
        </div>
        <div class="filter-product__item">
          <button>x</button>
          <span>Pen</span>
        </div>
        <div class="filter-product__item">
          <button>x</button>
          <span>Keyboard</span>
        </div>
        <div class="filter-product__item">
          <button>x</button>
          <span>Accessories</span>
        </div>
      </div>
    </div>
    <div class="products-side">
      <router-link
        class="products-item"
        v-for="product in products"
        :key="product.masp"
        :to="{ name: 'productDetail', params: { id: product.masp } }"
      >
        <div
          class="item-image"
          :style="{ backgroundImage: `url(${product.hinhanh})` }"
        ></div>
        <span>-20%</span>
        <div class="item-info">
          <div class="rating">
            <i class="fa-solid fa-star"></i>
            <i class="fa-solid fa-star"></i>
            <i class="fa-solid fa-star"></i>
            <i class="fa-solid fa-star"></i>
            <i class="fa-solid fa-star-half-stroke"></i>
          </div>
          <div class="item-cate">
            {{ product.maloai }}
          </div>
          <div class="item-name">
            {{ product.tensp }}
          </div>
          <div class="item-price">$ {{ product.gia }}</div>
        </div>
      </router-link>
    </div>
  </div>
  <Footer></Footer>
</template>

<script>
import Navbar from "./Navbar.vue";
import Footer from "./Footer.vue";
import shopFunction from "@/util/loginFunction/shopFunction";
import axios from "axios";
import { onMounted, ref } from "vue";
export default {
  components: {
    Navbar,
    Footer,
  },
  setup() {
    const products = ref();
    const fetchProducts = () => {
      axios
        .get("http://localhost/DACN-master/src/api/products.php")
        .then((res) => {
          products.value = res.data;
          console.log(products.value);
        })
        .catch((err) => {
          console.log("Error fetching data", err);
        });
    };
    onMounted(() => {
      fetchProducts();
    });
    return {
      products,
      fetchProducts,
    };
  },
};
</script>

<style>
@import "../../scss/products.scss";
</style>
