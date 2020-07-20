<template>
    <div class="product">
        
        <div class="product-image">
            <img :src='selectedGuitar' :alt='selectedGuitarAlt'/>
        </div>
        

        <div class="product-info">
        <h1>{{title}}</h1>

            <p v-if="currentGuitar <= 5 && currentGuitar > 0">Almost Out of Stock!!</p>
            <p v-else-if="currentGuitar >= 6">In Stock!!</p>
            <p v-else-if="currentGuitar === 0">Out Of Stock!!</p>

            <p v-if="premium">Free Shipping</p>
            <p v-else>Shiping $2.99</p>

            <li v-for="(detail,index) in details" :key="index">
                {{detail}}
            </li>
            
            <div class="guitarModels" v-for="(guitar, index) in guitars" 
            :key="guitar.model"
            :class="{activeGuitar: selectedGuitarIndex === index}"
            @mouseover="updateSelectedGuitarIndex(index)">
            {{guitar.model}}
            </div>

            <button 
            class="buttons"
            :disabled="!currentGuitar"
            :class="{inactiveButton: !currentGuitar}"
            @click="addToCart()">
            Add Item</button>

            <button 
            class="buttons"
            @click="removeFromCart()">
            Remove Item</button>

            
            <ReviewTabs :reviews="reviews" @add-review="addReview"/>

        </div>
    </div>
</template>

<script>
import ReviewTabs from '@/components/ReviewTabs.vue'
import {eventBus} from '../main'

    export default {
        name:"Products",
        components: {
          ReviewTabs
        },
        props: {
            premium: {
              type:Boolean,
              required:true  
            }
        },
        data() {
            return {
                guitarBrand: 'Manson',
                guitarTitle: 'Guitars',
                selectedGuitarIndex: 0,
                reviews:[],
                details: ['Made in England', 'Midi Controllers', 'Financing Available'],
                guitars: [
                    {
                      productID:0,
                      brand: 'Manson',
                      model: 'MB-1',
                      quantity: 7,
                      img:'mb-1',
                      alt:'mb-1',
                      onSale: true
                    },
                    {
                      productID:1,
                      brand: 'Manson',
                      model: 'CE-7',
                      quantity: 0,
                      img:'manson_ce-7',
                      alt:'ce-7',
                      onSale: true
                    }
                ]
            }
        },
        methods: {
            updateSelectedGuitarIndex(index) {
                this.selectedGuitarIndex = index
            },
            addToCart() {
                this.$emit('add-to-cart', this.guitars[this.selectedGuitarIndex].productID)
            },
            removeFromCart() {
                this.$emit('remove-from-cart', this.guitars[this.selectedGuitarIndex].productID)
            },
            addReview(reviewObj) {
                this.reviews.push(reviewObj)
            }
        },
        computed: {
            title() {
                return `${this.guitarBrand} ${this.guitarTitle}`
            },
            selectedGuitar() {
                const selectedProduct = this.guitars[this.selectedGuitarIndex].img
                //require(`../assets/manson_ce-7.jpg`)
                return require(`../assets/${selectedProduct}.jpg`)
            },
            selectedGuitarAlt() {
                return this.guitars[this.selectedGuitarIndex].alt
            },
            currentGuitar() {
                return this.guitars[this.selectedGuitarIndex].quantity
            }
        },
        created() {
          eventBus.$on('add-review', productReview => {
            this.reviews.push(productReview)
          })
        }
    }
</script>

<style lang="scss" scoped>
.product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
}

.product-image,
.product-info {
    margin-top: 10px;
    width: 50%;
}

.guitarModels {
    width:10%;
}

.activeGuitar {
    text-decoration: underline;
    color:springgreen;
}

.activeTab {
    text-decoration: underline;
    color:blue;
}

.inactiveButton {
    background-color:grey;
}

button {
    margin:10px;
    margin-left: 0px;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  }

.cart {
    float:right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
}

img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
}

</style>