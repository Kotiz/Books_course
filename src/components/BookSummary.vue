<script>
import { ref } from 'vue'
export default {
  name: 'BooksSummary',
  setup () {
    const priceSummary = ref(0)
    return { priceSummary }
  },
  props: {
    books: {
      type: Array,
      required: true
    },
    booksFromApi: {
      type: Array,
      required: true
    },
    bestSeller1: {
      type: Object,
      required: false
    },
    bestSeller2: {
      type: Object,
      required: false
    },
    bestSeller3: {
      type: Object,
      required: false
    }
  },
  // methods: {
  //   increaseRating (bestSellerKey) {
  //     switch (bestSellerKey) {
  //       case 'jeden':
  //         this.bestSeller1.rating++
  //         break
  //       case 'dwa':
  //         this.bestSeller2.rating++
  //         break
  //       case 'trzy':
  //         this.bestSeller3.rating++
  //         break
  //     }
  //   },
  //   decreaseRating (bestSellerKey) {
  //     switch (bestSellerKey) {
  //       case 'jeden':
  //         this.bestSeller1.rating--
  //         break
  //       case 'dwa':
  //         this.bestSeller2.rating--
  //         break
  //       case 'trzy':
  //         this.bestSeller3.rating--
  //         break
  //     }
  //   }
  // },
  computed: {
    bookAmount () {
      if (!this.books) return 0
      return this.books.length
    },
    totalPrice () {
      if (!this.books) return 0
      const priceSummary = this.books.reduce((sum, next) => sum + next.price, 0)
      return priceSummary
    },
    totalPrice2 () {
      if (!this.books) return 0
      const priceSummary = this.books.reduce((sum, next) => sum + parseFloat(next.price.substring(1)), 0)
      return parseFloat((priceSummary).toFixed(10))
    }
  }
}
</script>
<template>
  <hr>
    <div class="books-list">Books Amount : {{ bookAmount }}</div>
    <!-- <div>Total price : {{ totalPrice }} </div> -->
    <div class="books-list">Total price : {{ totalPrice2 }} </div>
    <br />
    <!-- <span v-if="bestSeller1 && bestSeller2 && bestSeller3">
      <p>best 1:{{ bestSeller1.name }}</p><button @click="increaseRating('jeden')">+</button><button @click="decreaseRating('jeden')">-</button>
      <p>best 2:{{ bestSeller2.name }}</p><button  @click="increaseRating('dwa')">+</button><button @click="decreaseRating('jeden')">-</button>
      <p>best 3:{{ bestSeller3.name }}</p><button @click="increaseRating('trzy')">+</button><button @click="decreaseRating('jeden')">-</button>
    </span> -->
</template>
