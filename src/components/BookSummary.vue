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
    }
  },
  computed: {
    bookAmount () {
      return this.books.length
    },
    // totalPrice () {
    //   return this.books.forEach((book) => { (this.priceSummary += book.price) })
    // }
    totalPrice () {
      const priceSummary = this.books.reduce((sum, next) => sum + next.price, 0)
      return priceSummary
    }
  }
}
</script>
<template>
    <div>Books Amount : {{ bookAmount }}</div>
    <div>Total price : {{ totalPrice }} </div>
</template>
<style>
div {
    padding: 5px;
}
</style>
