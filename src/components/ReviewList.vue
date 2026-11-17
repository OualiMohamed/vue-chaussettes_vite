<script>
export default {
  name: 'ReviewList',
  props: {
    reviews: {
      type: Array,
      required: true,
    },
  },
}
</script>

<template>
  <div class="review-container">
    <h3>Commentaires</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        <strong>{{ review.name }}</strong> a donné {{ review.rating }} étoiles
        <br />
        <em>"{{ review.review }}"</em>
        <br />
        Recommandé: {{ review.recommend }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
.review-container {
  width: 425px;
  padding: 20px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 20px -12px rgba(0, 0, 0, 0.57);
  margin-left: 40px;
  border: 2px solid #d8d8d8;
}

.review-container li {
  margin-bottom: 30px;
}
</style>
