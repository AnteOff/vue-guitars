<template>
    <div>
      
      <span v-for="reviewTab in reviewTabs" :key="reviewTab"
          class="tabs"
          :class="{activeTab: selectedReviewTab === reviewTab}"
          @click="switchTab(reviewTab)"
          >{{reviewTab}}</span>
      
      <ul>
        <li v-for="(review, index) in reviews" :key="index" v-show="selectedReviewTab === 'Reviews'">
          <p>{{review.name}}</p>
          <p>{{review.review}}</p>
          <p>Rating: {{review.rating}}</p>
          <p>{{review.reccomendation}}</p>
        </li>
      </ul>

      <span v-if="!this.reviews.length">There are no reviews for this product yet</span>

      <ProductReviewsForm v-show="selectedReviewTab === 'Product Reviews'"/>
    </div>
</template>

<script>
import ProductReviewsForm from '@/components/ProductReviewsForm.vue'

    export default {
      components: {
        ProductReviewsForm
      },
      props: {
        reviews: {
          type: Array,
          required: true
        }
      },
      data() {
        return {
          reviewTabs:['Reviews', 'Product Reviews'],
          selectedReviewTab: 'Reviews'
        }
      },
      methods: {
        switchTab(selectedTab) {
          this.selectedReviewTab = selectedTab
        }
      }
    }
</script>

<style lang="scss" scoped>
  .activeTab {
    color:blue;
    text-decoration: underline;
  }
  .tabs {
    cursor: pointer;
    margin-left: 20px;
  }
</style>