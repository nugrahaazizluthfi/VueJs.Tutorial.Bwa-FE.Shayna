<template>
  <div class="home">
    <!-- Header Section Begin -->
    <HeaderShayna />
    <!-- Header End -->

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <a href="./home.html"><i class="fa fa-home"></i> Home</a>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="gambar_default" alt="" />
                </div>
                <div
                  class="product-thumbs"
                  v-if="productDetail.galleries.length > 0"
                >
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :dots="false"
                    :nav="false"
                  >
                    <div
                      v-for="thumb in productDetail.galleries"
                      :key="thumb.id"
                      :class="
                        `pt ${thumb.foto == gambar_default ? 'active' : ''}`
                      "
                      @click="changeImage(thumb.foto)"
                    >
                      <img :src="thumb.foto" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-left">
                  <div class="pd-title">
                    <span>{{ productDetail.type }}</span>
                    <h3>{{ productDetail.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <div v-html="productDetail.description"></div>
                    <h4>$ {{ productDetail.price }}</h4>
                  </div>
                  <div class="quantity">
                    <!-- <router-link to="/cart" class="primary-btn pd-cart"> -->
                    <a
                      href="#"
                      @click="
                        saveKeranjang(
                          productDetail.id,
                          productDetail.name,
                          productDetail.price,
                          gambar_default
                        )
                      "
                      class="primary-btn pd-cart"
                      >Add To Cart</a
                    >
                    <!-- </router-link> -->
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->

    <!-- Footer Section Begin -->
    <RelatedShayna />
    <!-- Footer Section End -->

    <!-- Related Products Section End -->
    <FooterShayna />
    <!-- Related Products Section End -->
  </div>
</template>

<script>
import carousel from "vue-owl-carousel";

// @ is an alias to /src
import HeaderShayna from "@/components/HeaderShayna.vue";
import FooterShayna from "@/components/FooterShayna.vue";
import RelatedShayna from "@/components/RelatedShayna.vue";

import axios from "axios";

export default {
  name: "Product",
  components: {
    HeaderShayna,
    FooterShayna,
    RelatedShayna,
    carousel,
  },
  data() {
    return {
      gambar_default: "img/mickey1.jpg",
      productDetail: [],
      keranjangUser: [],
    };
  },
  methods: {
    changeImage(urlImage) {
      this.gambar_default = urlImage;
      console.log(this.productId);
    },
    setDataPicture(data) {
      let picDefault = data.filter((data) => data.is_default == 1);
      this.gambar_default = picDefault[0].foto;
    },
    saveKeranjang(id, name, price, foto) {
      let productStored = { id, name, price, foto };

      this.keranjangUser.push(productStored);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);
      this.$router.go(this.$router.currentRoute);
    },
  },
  mounted() {
    if (localStorage.getItem("keranjangUser")) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (error) {
        localStorage.removeItem("keranjangUser");
      }
    }

    axios
      .get("http://localhost:8000/api/products/", {
        params: {
          id: this.$route.params.id,
        },
      })
      .then((res) => {
        const { data } = res.data;
        this.productDetail = data;
        this.setDataPicture(data.galleries);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
.product-thumbs .pt {
  margin-right: 14px;
}
</style>
