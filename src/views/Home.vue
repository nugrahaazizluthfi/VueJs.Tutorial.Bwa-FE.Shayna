<template>
  <div class="home">
    <!-- Header Section Begin -->
    <HeaderShayna />
    <!-- Header End -->

    <!-- Hero Section Begin -->
    <HeroShayna />
    <!-- Hero Section End -->

    <!-- Women Banner Section Begin -->
    <WomenShayna />
    <!-- Women Banner Section End -->

    <!-- Instagram Section Begin -->
    <InstaShayna />
    <!-- Instagram Section End -->

    <!-- Partner Logo Section Begin -->
    <PartnerShayna />
    <!-- Partner Logo Section End -->

    <!-- Footer Section Begin -->
    <FooterShayna />
    <!-- Footer Section End -->
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderShayna from "@/components/HeaderShayna.vue";
import HeroShayna from "@/components/HeroShayna.vue";
import WomenShayna from "@/components/WomenShayna.vue";
import InstaShayna from "@/components/InstaShayna.vue";
import PartnerShayna from "@/components/PartnerShayna.vue";
import FooterShayna from "@/components/FooterShayna.vue";

export default {
  name: "Home",
  components: {
    HeaderShayna,
    HeroShayna,
    WomenShayna,
    InstaShayna,
    PartnerShayna,
    FooterShayna,
  },
};
</script>
