<script setup>
import { onMounted, ref, computed, watch } from 'vue';
// import defaultLayouts from './components/layouts/defaultLayouts.vue';
const Products = ref([])
const rating = ref([])
const counter = ref(1)
const Product = computed(() => Products.value)
const rate = computed(() => rating.value)
const HandleNext = () => counter.value++
const ratingClothes = computed(() => Math.round(rating.value))
const loading = ref(false)
onMounted(async () => {
  watch(counter, async (newValue) => {
    newValue === 20 ? counter.value = 1 : ''
    loading.value = true
    try {
      const response = await fetch(`https://fakestoreapi.com/products/${newValue}`)
      const data = await response.json();
      Products.value = data
      rating.value = data.rating.rate
    } catch (error) {
      console.error(error);
    } finally {
      loading.value = false;
    }
  })
  if (Products.value.length === 0) {
    loading.value = true
    try {
      const response = await fetch(`https://fakestoreapi.com/products/1`)
      const data = await response.json();
      Products.value = data
      rating.value = data.rating.rate
    } catch (error) {
      console.error(error);
    }
    finally {
      loading.value = false
    }
  }
})
</script>

<template>
  <main
    :class="[Product.category === `men's clothing` ? 'bg-male polygon' : Product.category === `women's clothing` ? 'bg-female polygon' : 'bg-notfound polygon']">
    <section
      :class="[loading ? 'figure-clothes-single container' : Product.category === `men's clothing` || Product.category === `women's clothing` || !loading ? 'figure-clothes container' : 'container cards']">
      <!-- products -->
      <div v-if="loading" class="spiner">
        <span class="loader"></span>
      </div>
      <aside v-if="!loading"
        :class="[Product.category === `men's clothing` || Product.category === `women's clothing` ? 'block' : 'hidden']">
        <figure class="figure-img">
          <img :src="Product.image" :alt="Product.title" loading="eager" width="305px" height="407px">
        </figure>
      </aside>
      <article v-if="!loading"
        :class="[Product.category === `men's clothing` || Product.category === `women's clothing` ? 'block card-text' : 'hidden']">
        <h1 :class="[Product.category === `men's clothing` ?
      'card-title title-male' : Product.category === `women's clothing`
        ? 'card-title title-female' : '']">
          {{ Product.title }}
        </h1>
        <section class="wrapper-category">
          <header>
            <h2 class="card-category">
              {{ Product.category }}
            </h2>
          </header>
          <footer class="rate-wrapper">
            <h2 class="card-category">
              {{ rate }}/5
            </h2>
            <section v-if="ratingClothes === 5">
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
            </section>
            <section v-else-if="ratingClothes === 4">
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
            </section>
            <section v-else-if="ratingClothes === 3">
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
            </section>
            <section v-else-if="ratingClothes === 2">
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
            </section>
            <section v-else>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
              <span :class="[Product.category === `men's clothing` ? 'rate-icon rate-null-male' :
      Product.category === `women's clothing` ? 'rate-icon rate-null-female' : '']">
              </span>
            </section>
          </footer>
        </section>
        <hr>
        <p class="card-description">
          {{ Product.description }}
        </p>
        <hr>
        <span :class="[Product.category === `men's clothing` ? 'card-title title-male price' :
      Product.category === `women's clothing` ? 'card-title title-female price' : ''
    ]">
          ${{ Product.price }}
        </span>
        <aside class="btn-wrapper">
          <section>
            <button :class="[Product.category === `men's clothing` ? 'btn btn-male' : 'btn btn-female']">
              Buy
            </button>
          </section>
          <section>
            <button :class="[Product.category === `men's clothing` ? 'btn btn-male-next' : 'btn btn-female-next']"
              @click="HandleNext">
              Next
            </button>
          </section>
        </aside>
      </article>
      <!-- end producst -->
      <!-- notFOund -->
      <div v-if="!loading"
        :class="[Product.category !== `men's clothing` && Product.category !== `women's clothing` ? 'block' : 'hidden']"
        class="figure-notFound">
        <div class="figure-logo">
          <h1 class="card-category">
            This product is unavailable to show
          </h1>
          <div class="btn-not">
            <button @click="HandleNext" class="btn btn-notfound-next">
              Next product
            </button>
          </div>
        </div>
      </div>
      <!-- notFound -->
    </section>
  </main>

</template>


<style scoped></style>