<script>
import BooksList from './components/BooksList.vue'
import BooksLengthMsg from './components/BooksLengthMsg.vue'
import booksSummary from './components/BookSummary.vue'
import BookForm from './components/BookForm.vue'
// import { response } from 'express'
// import booksItem from './components/BooksItems.vue'
export default {
  components: { BooksList, BooksLengthMsg, booksSummary, BookForm },
  name: 'App',
  data: () => ({
    books: [
      {
        title: 'Windows Powershell w miesiąc',
        price: 20
      },
      {
        title: 'Alicja w krainie czarów',
        price: 18
      },
      {
        title: 'Dracula',
        price: 10
      }
    ],
    booksApi: []
  }),
  methods: {
    addBook (book) {
      this.books.push({ ...book })
    },
    removeBook (index) {
      this.books.splice(index, 1)
      console.log('delete', index)
    },
    resetForm () {
      this.form.price = null
      this.form.title = ''
    },
    getBooks () {
      fetch('https://api.itbook.store/1.0/search/mongodb')
        .then(response => response.json())
        .then(data => (this.booksApi = data))
    }
  }
}
</script>
<template>
  <div class="app">
    <header>
      <h1 class="app__heading">Books<span>.app</span></h1>
    </header>
  <div v-for="book in booksApi" :key="book">
    <span>{{ booksApi.books }}</span>
  </div>
    <button @click="getBooks">Show Books</button>
    <books-list @remove="removeBook" :books="books" />
    <books-length-msg :books="books"/>
    <book-form @add="addBook"/>
  </div>
  <books-summary :books="books" />
  <hr>
</template>
<style lang="scss">
  .app {
    width: 100%;
    max-width: 1000px;
    padding: 2rem;
    margin: 0 auto;
    &__heading {
      font-size: 3rem;
      text-align: center;
      span {
        color: #5a58da;
      }
    }
  }
  </style>
