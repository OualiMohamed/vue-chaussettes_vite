<script>
import ProductDetails from './ProductDetails.vue'
import ReviewForm from './ReviewForm.vue'
import ReviewList from './ReviewList.vue'

// 1. Import your images here
import socksGreen from '@/assets/images/socks_green.jpg'
import socksBlue from '@/assets/images/socks_blue.jpg'

export default {
  name: 'ProductDisplay',
  components: {
    ProductDetails,
    ReviewForm,
    ReviewList,
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  }, // <--- Close props here!

  data() {
    return {
      brand: 'VueJS',
      product: 'Chaussettes',
      description:
        'Cette paire est composée de chaussettes Marines et Vertes dépareillées avec un design différent de chaque côté!, sur le pied gauche une feuille. Humour et originalité assurés sur ces chaussettes.',
      selectedVariant: 0,
      url: 'https://vuejs.org/',
      inventory: 100,
      onSale: true,
      details: ['50% coton', '30% laine', '20% polyester'],
      variants: [
        { id: 2001, color: 'green', image: socksGreen, quantity: 50 },
        { id: 2002, color: 'blue', image: socksBlue, quantity: 5 },
      ],
      sizes: [39, 42, 43, 46],
      myStyle: {
        color: 'red',
        fontSize: '56px',
      },
      reviews: [],
    }
  },

  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].id)
    },
    updateVariant(index) {
      this.selectedVariant = index
      console.log(index)
    },
    removeFromCart() {
      this.$emit('remove-from-cart', this.variants[this.selectedVariant].id)
    },
    addReview(review) {
      this.reviews.push(review)
      console.log(this.reviews)
    },
  },

  computed: {
    title() {
      return this.brand + ' ' + this.product
    },
    image() {
      return this.variants[this.selectedVariant].image
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity
    },
    sale() {
      if (this.onSale) {
        return this.brand + ' ' + this.product + ' est en vente'
      }
      return ''
    },
    shipping() {
      if (this.premium) {
        return 'Gratuit'
      }
      return '8DT'
    },
  },
}
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <!-- une image -->
        <img :class="{ imageStyle: !inStock }" :src="image" v-bind:alt="product" />
        <!-- <img :src="inStock ? image : 'assets/images/out-of-stock-img.png'" v-bind:alt="product" /> -->
      </div>
      <div class="product-info">
        <h1 :style="myStyle">{{ title }}</h1>
        <p>{{ sale }}</p>
        <p>Expédition: {{ shipping }}</p>
        <a :href="url">VueJS</a>
        <p>{{ description }}</p>
        <!-- <p v-if="inStock">En Stock</p>
        <p v-else>En rupture de stock</p> -->
        <p v-if="inventory > 10">En Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Presque épuisé</p>
        <p v-else>En rupture de stock</p>
        <p v-if="onSale">En Vente!</p>
        <ProductDetails :details="details" />
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
          class="color-circle"
          v-bind:style="{ backgroundColor: variant.color }"
        ></div>
        <div class="pointure">
          <label for="pointure">Pointure </label>
          <select id="pointure">
            <option v-for="size in sizes">{{ size }}</option>
          </select>
        </div>
        <div>
          <button
            class="button"
            @click="addToCart"
            :disabled="inStock == false"
            :class="{ disabledButton: inStock == false }"
          >
            Add to cart
          </button>
          <button
            class="button"
            @click="removeFromCart"
            :disabled="inStock == false"
            :class="{ disabledButton: inStock == false }"
          >
            Remove from cart
          </button>
        </div>
      </div>
    </div>
    <ReviewList v-if="reviews.length" :reviews="reviews" />
    <ReviewForm @review-submitted="addReview" />
  </div>
</template>

<style>
.product-display {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  width: 100%;
}

.product-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.product-image,
.product-info {
  width: 50%;
}

.imageStyle {
  filter: grayscale(100%) blur(5px);
}

.button {
  margin: 30px;
  background-color: #39495c;
  border-radius: 5px;
  font-size: 18px;
  /* width: 160px; */
  height: 60px;
  color: white;
  padding: 20px;
  box-shadow:
    inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}

.cart {
  margin: 25px 100px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 10px 30px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.color-circle {
  width: 50px;
  height: 50px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
}

.disabledButton {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

img {
  border: 2px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  padding: 15px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

ul {
  list-style-type: none;
}
</style>
