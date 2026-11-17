<script>
export default {
  name: 'ReviewForm',
  data() {
    return {
      name: '',
      review: '',
      rating: null,
      recommend: null,
    }
  },
  methods: {
    onSubmit() {
      if (
        this.name === '' ||
        this.review === '' ||
        this.rating === null ||
        this.recommend === null
      ) {
        alert('Commentaire incomplet. SVP remplissez les champs.')
        return
      }

      let productReview = {
        name: this.name,
        review: this.review,
        rating: this.rating,
        recommend: this.recommend,
      }

      this.$emit('review-submitted', productReview)

      this.name = ''
      this.review = ''
      this.rating = null
      this.recommend = null
    },
  },
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Laisser un commentaire</h3>
    <label for="name">Name</label>
    <input type="text" id="name" v-model="name" />

    <label for="review">Commentaire</label>
    <textarea id="review" v-model="review"></textarea>

    <label id="rating">Evaluation</label>
    <select for="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <label for="recommend">Recommanderiez-vous ce produit?</label>
    <select id="recommend" v-model="recommend">
      <option>Oui</option>
      <option>Non</option>
    </select>

    <input type="submit" class="button" value="Envoyer" />
  </form>
</template>

<style scoped>
input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
}

input[type='submit'] {
  height: 100%;
}

label {
  font-size: 20px;
  margin-bottom: 5px;
}

li {
  font-size: 18px;
}

.review-form {
  display: flex;
  flex-direction: column;
  width: 425px;
  padding: 20px;
  margin: 40px;
  border: 2px solid #d8d8d8;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}
.review-form .button {
  display: block;
  margin: 30px auto;
}

select {
  height: 40px;
  font-size: 20px;
  background-color: white;
  cursor: pointer;
}

textarea {
  width: 95%;
  height: 70px;
  padding: 10px;
  font-size: 20px;
  margin-bottom: 20px;
}
</style>
