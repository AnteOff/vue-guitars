<template>
    <div>
      <form class="review-form" @submit.prevent="submitForm">
        <p v-if="this.errors.length">
          <b>Please correct the following errors:</b>
          <ul>
            <div v-for="(error, index) in errors" :key="index">
              {{ error }}
            </div>
          </ul>
        </p>

        <p>
          <label for="name:">Name:</label>
          <input class="textInput" type="text" id="name" v-model="name">
        </p>
        <p>
          <label for="review">Review: </label>
          <textarea id="review" v-model="review"></textarea>
        </p>

        <p>
        <label for="rating"></label>
        <select id="rating" v-model="rating">
          <option>5</option>
          <option>4</option>
          <option>3</option>
          <option>2</option>
          <option>1</option>
        </select>
        </p>
        <span>Would you reccomend this product?</span>
        <br>
        <input type="radio" id="yes" value=true v-model="recommendation">
        <label for="yes">yes</label>
          <br>
        <input type="radio" id="no" value=false v-model="recommendation">
        <label for="no">no</label>
          <br>
        <input type="submit" value="submit">
      </form>
    </div>
</template>

<script>
import {eventBus} from '../main'

    export default {
      data() {
        return {
          name: null,
          review: null,
          rating: null,
          recommendation: null,
          errors: []
        }
      },
      methods: {
        submitForm() {
        this.errors = []
        if (this.name && this.review && this.rating && this.recommendation) {
            const submitObj = {
            name: this.name,
            review: this.review,
            rating: this.rating,
            recommendation: this.recommendation
          } 
            eventBus.$emit('add-review', submitObj)
            this.name = null
            this.review = null
            this.rating = null
            this.recommendation = null
        } else {
          if (!this.errors.length) {
            if (!this.name) this.errors.push('Name Required')
            if (!this.review) this.errors.push('Please enter a review')
            if (!this.rating) this.errors.push('Please leave a rating')
            if (!this.recommendation) this.errors.push('Please add a reccomendation')
          }
        }
      }
      }
    }
</script>

<style lang="scss" scoped>
  .review-form {
    width: 400px;
    padding: 20px;
    border: 1px solid #d8d8d8;
  }

  textarea {
    width: 100%;
    height: 40px;
  }

  .textInput {
    width: 100%;
    height: 25px;
  }
  
</style>