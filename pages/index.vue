<template>
  <main class="container">
    <page-intro
      :image="'/logo-long.svg'"
      :alt="'Company logo'"
      :subtitle="'Between hope and possible, there’s a bridge'"
      :video="'/expl.mp4'"
      :loop="false"
    />
    <section class="vertical strong">
      <h2>Areas</h2>
      <div class="cards">
        <card-preview
          v-for="area in data.areas"
          :key="area.id"
          :title="area.title"
          :image="`data:image/png;base64,${area.main_image}`"
          :alt="`Image of ${area.title}`"
          :link="`/areas/${area.id}`"
        />
      </div>
    </section>
    <section class="vertical">
      <h2>Best sellers</h2>
      <div class="cards">
        <card-preview
          v-for="product in data.products"
          :key="product.id"
          :title="product.title"
          :image="`data:image/png;base64,${product.image}`"
          :alt="`Image of ${product.title}`"
          :link="`/products/${product.id}`"
        />
      </div>
    </section>
    <section class="vertical strong">
      <h2>Our partners</h2>
      <div class="cards">
        <a href="https://www.cisco.com/" title="Image of Cisco"
          ><img
            class="partners"
            src="https://www.freepnglogos.com/uploads/cisco-png-logo/new-cisco-logo-png-1.png"
            alt="new cisco logo png"
        /></a>
        <a href="https://www.google.com/" title="Image of Google"
          ><img
            class="partners"
            src="https://www.freepnglogos.com/uploads/new-google-logo-png-0.png"
            alt="google logos png"
        /></a>
        <a href="https://www.netflix.com" title="Image of Netflix"
          ><img
            class="partners"
            src="https://www.freepnglogos.com/uploads/netflix-logo-0.png"
            alt="netflix logo"
        /></a>
        <a href="https://www.microsoft.com" title="Image of Microsoft"
          ><img
            class="partners"
            src="https://www.freepnglogos.com/uploads/microsoft-logo-png-transparent-background-1.png"
            alt="microsoft logo png transparent background"
        /></a>
      </div>
    </section>
  </main>
</template>

<script>
import CardPreview from '~/components/CardPreview.vue'
import PageIntro from '~/components/PageIntro.vue'
export default {
  components: { CardPreview, PageIntro },
  async asyncData({ $axios }) {
    const areas = (await $axios.get('/api/areas')).data
    const products = (await $axios.get('/api/products')).data.slice(10, 14)
    const data = { areas, products }
    return { data }
  }
}
</script>

<style scoped>
div.image img {
  width: 450px;
  height: auto;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

div.slogan h3 {
  color: white;
}

img.partners {
  width: 200px;
  height: auto;
  display: block;
  padding: 50px;
}

@media (max-width: 500px) {
  img.partners {
    width: 100px;
    padding-inline: 10px;
    padding-top: 25px;
    padding-bottom: 25px;
  }
}
</style>
