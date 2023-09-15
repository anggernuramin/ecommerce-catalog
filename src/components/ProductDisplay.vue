<template>
  <section id="category-women" class="container">
    <div class="bg-product" :class="category" v-if="data">
      <div class="wrapper-card">
        <div class="card">
          <div class="card-image">
            <img :src="data.image" :alt="data.title" />
          </div>
          <div class="card-content">
            <h2>{{ data.title.substring(0, 68) }}</h2>
            <div class="card-content-category">
              <h5>{{ data.category }}</h5>
              <div class="rating">
                <h5>{{ data.rating.rate }}/5</h5>
                <div class="card-product-rating">
                  <div v-for="(star, index) in 5" :key="index" class="rating-circle" :class="{ 'active-rating': index < roundedRating, 'half-rating': index === roundedRating - 0.5 }"></div>
                </div>
              </div>
            </div>
            <p>{{ data.description.substring(0, 340) }}</p>
            <h5 class="price">${{ data.price }}</h5>
            <div class="card-content-button">
              <button class="button-active">Buy now</button>
              <button @click="getNumberId" class="button-next-product">Next product</button>
            </div>
          </div>
        </div>
      </div>
      <div v-if="data.category !== 'women\'s clothing' && data.category !== 'men\'s clothing'">
        <div class="wrapper-card bg-unavailable-product">
          <div class="card">
            <h2>This product is unavailable to show</h2>
            <button @click="getNumberId">Next product</button>
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="bg-product bg-skeleton">
        <div class="wrapper-card">
          <SkeletonProduct />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import SkeletonProduct from "./SkeletonProduct.vue";

export default {
  name: "ProductDisplay",
  components: {
    SkeletonProduct,
  },
  data() {
    return {
      numberId: 2,
      data: null, // declare variable data untuk menampung setiap data product dari api
      rating: null, // declare rating dengan nilai null
    };
  },
  mounted() {
    setTimeout(() => {
      this.getProduct(1);
    }, 3000);
  },
  computed: {
    category() {
      if (this.data.category === "women's clothing") {
        return "bg-category-women";
      } else if (this.data.category === "men's clothing") {
        return "bg-category-men";
      } else {
        return "unavailable-product";
      }
    },
    roundedRating() {
      if (this.rating === null) {
        return 0; // Rating default jika data belum tersedia
      }

      const decimalPart = this.rating % 1;

      if (decimalPart <= 0.3) {
        return Math.floor(this.rating);
      } else if (decimalPart >= 0.4 && decimalPart <= 0.8) {
        return Math.floor(this.rating) + 0.5;
      } else {
        return Math.ceil(this.rating);
      }
    },
  },
  methods: {
    getNumberId() {
      if (this.numberId === 20) {
        this.numberId = 1;
      }
      this.getProduct(this.numberId++);
    },
    async getProduct(id) {
      try {
        const request = await fetch(`https://fakestoreapi.com/products/${id}`);
        const response = await request.json();
        this.rating = Number(response.rating.rate);
        this.data = response;
      } catch (error) {
        console.log(error.message);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
/* style page product start */
.bg-category-women {
  background-image: url("../assets/bg-pattern.svg");
}
.bg-category-women::after {
  background-color: var(--bg-women-style-color);
}
.bg-category-men {
  background-image: url("../assets/bg-pattern.svg");
}
.bg-category-men::after {
  background-color: var(--bg-men-style-color);
}

.card {
  overflow: hidden !important;
  display: grid;
  width: 100%;
  height: 100%;
  gap: 20px;
  grid-template-columns: 1.3fr 2fr;
  justify-content: center;
  align-items: flex-start;
}
.card .card-image {
  width: 80%;
  height: 350px;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  margin: auto;
}
.card .card-image img {
  width: 100%; /* Lebar gambar akan mengisi lebar kontainer */
  height: 100%; /* Tinggi gambar akan mengisi tinggi kontainer */
  object-fit: cover; /* Mempertahankan rasio aspek gambar */
}
.card .card-content {
  min-height: 300px;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  flex-direction: column;
  padding: 20px;
}
.card-content h2 {
  height: 75px;
  font-size: 28px;
  font-weight: 600;
  line-height: 33.89px;
  margin-bottom: 10px;
}
.bg-category-women .card-content h2 {
  color: var(--women-style-color);
}
.bg-category-men .card-content h2 {
  color: var(--men-style-color);
}

.card-content .card-content-category {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}
.card-content-category .rating {
  display: flex;
  justify-content: center;
  align-items: center;
}
.card-content-category h5 {
  font-weight: 400;
  font-size: 18px;
  line-height: 21.78px;
  color: var(--text-secondary);
}
.card-content-category .rating {
  display: flex;
  gap: 5px;
  justify-content: center;
  align-items: center;
}
.card-product-rating {
  display: flex;
  gap: 2px;
}
.card-product-rating .rating-circle {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
.bg-category-women .card-product-rating .rating-circle {
  border: 2px solid var(--women-style-color);
}
.bg-category-men .card-product-rating .rating-circle {
  border: 2px solid var(--men-style-color);
}

.bg-category-women .card-product-rating .active-rating {
  background: var(--women-style-color);
}
.bg-category-men .card-product-rating .active-rating {
  background: var(--men-style-color);
}

.bg-category-women .card-product-rating .half-rating {
  background: linear-gradient(90deg, var(--women-style-color) 50%, var(--primary-color) 50%);
}
.bg-category-men .card-product-rating .half-rating {
  background: linear-gradient(90deg, var(--men-style-color) 50%, var(--primary-color) 50%);
}
.card-product-rating i {
  color: red;
}
.card-product-rating .active-rating {
  color: gold;
}
.card-content p {
  width: 100%;
  height: 170px;
  border-block: 2px solid rgba(0, 0, 0, 0.1);
  padding-block: 20px;
  font-size: 20px;
  font-weight: 400;
  line-height: 24.2px;
  color: var(--text-primary);
  margin-bottom: 20px;
  overflow-y: auto;
}
.card-content .price {
  font-size: 28px;
  font-weight: 600;
  line-height: 33.89px;
  margin-bottom: 20px;
}
.bg-category-women .card-content .price {
  color: var(--women-style-color);
}
.bg-category-men .card-content .price {
  color: var(--men-style-color);
}

.card-content-button {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}
.card-content-button button {
  width: 259px;
  height: 42px;
  border-radius: 4px;
  text-align: center;
  font-weight: 600;
  font-size: 18px;
  line-height: 24.2px;
  cursor: pointer;
  transition: 0.3s;
}

.bg-category-women .card-content-button button {
  border: 2px solid var(--women-style-color);
  color: var(--women-style-color);
  background-color: var(--primary-color);
}
.bg-category-men .card-content-button button {
  border: 2px solid var(--men-style-color);
  color: var(--men-style-color);
  background-color: var(--primary-color);
}

.bg-category-women .card-content-button .button-active {
  color: var(--primary-color);
  background-color: var(--women-style-color);
}
.bg-category-women .card-content-button .button-active:hover {
  color: var(--women-style-color);
  background-color: transparent;
  border: 2px solid var(--women-style-color);
}

.bg-category-men .card-content-button .button-active {
  color: var(--primary-color);
  background-color: var(--men-style-color);
}
.bg-category-men .card-content-button .button-active:hover {
  color: var(--men-style-color);
  background-color: transparent;
  border: 2px solid var(--men-style-color);
}

.bg-category-women .card-content-button .button-next-product:hover {
  background-color: var(--women-style-color);
  border: 2px solid transparent;
  color: var(--primary-color);
}
.bg-category-men .card-content-button .button-next-product:hover {
  background-color: var(--men-style-color);
  border: 2px solid transparent;
  color: var(--primary-color);
}
/* style page product end */

/* style page unavailable start */
.unavailable-product {
  background-color: var(--bg-unavailable);
}
.bg-unavailable-product {
  background-image: url(../assets/sad-face.png);
  background-repeat: no-repeat;
  background-size: 1000px;
  background-position: 82px 32px;
}
.bg-unavailable-product .card {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100%;
  gap: 15px;
}
.bg-unavailable-product .card h3 {
  font-weight: 400;
  font-size: 20px;
  line-height: 24.2px;
}
.bg-unavailable-product .card button {
  cursor: pointer;
  transition: 0.3s;
  font-weight: 400;
  font-size: 18px;
  text-align: center;
  width: 465px;
  height: 34px;
  border-radius: 4px;
  background-color: var(--primary-color);
  border: 3px solid rgba(0, 0, 0, 0.4);
  margin-bottom: 70px;
}
.bg-unavailable-product .card button:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
/* style page unavailable end */
/* style skeleton start */
.bg-skeleton {
  background-color: #ddd;
  animation: loading 1.5s infinite;
}
@keyframes loading {
  0% {
    opacity: 0.7;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0.7;
  }
  /* style skeleton end*/
}
</style>
