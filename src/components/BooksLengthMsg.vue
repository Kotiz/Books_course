<script>
export default {
  name: 'BooksLengthMsg',
  props: {
    books: {
      type: Array,
      required: true
    }
  }
}
</script>
<template>
    <div>
      <p v-if="books.length < 1">Get some books !</p>
      <p v-else-if="books.length > 5 "> No. of books : {{ books.length }}</p>
      <p v-else-if="books.length <= 5 && books.length > 1 ">Not to many of them...</p>
      <p v-else-if="books.length == 1 ">One single book</p>
    </div>
</template>
