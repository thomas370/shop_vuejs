<template>
  <div>
    <h1 class="wrapper">{{ pageTitle }}</h1>
     <ul class="wrapper item-grid">
        <li v-for="product in productsByGender" :key="product.id" class="item-grid__item">
          <router-link :to="{ name: 'product', params: { id: product.id}}">
            <img class="product-image" :src="makeImagePath(product)" alt="">
            <p class="product-title">{{ product.name }}</p>
            <p><em>${{ product.price }}</em></p>
          </router-link>
        </li>
      </ul>
  </div>
</template>

<script>
import { imagePath } from '@/mixins/imagePath.js'

export default {
  name: 'women',
  mixins: [imagePath],
  data () {
    return {
      randomTopId: null,
      randomBottomId: null,
      randomFootwearId: null
    }
  },
  computed: {
    gender () {
      return this.$route.params.gender
    },
    pageTitle () {
      return `${this.gender[0].toUpperCase()}${this.gender.slice(1)}`
    },
    productsByGender () {
      return this.$store.getters.productsByGender(this.gender)
    }
  }
}
</script>

<style lang="scss">
.item-grid {
  list-style: none;
  padding-left: 0;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  flex-wrap: wrap;
}
.item-grid__item {
  box-sizing: border-box;
  text-align: center;
  padding: 1rem;
  flex: 0 0 33.3%;
  @media only screen and (max-width: 832px) {
    flex: 0 0 50%;
  }
  @media only screen and (max-width: 475px) {
    flex: 0 0 100%;
  }
}
</style>
