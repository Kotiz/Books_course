<script>
import BooksList from './components/BooksList.vue'
import BooksLengthMsg from './components/BooksLengthMsg.vue'
import booksSummary from './components/BookSummary.vue'
import BookForm from './components/BookForm.vue'
import BooksItemsVue from './components/BooksItems.vue'
export default {
  components: { BooksList, BooksLengthMsg, booksSummary, BookForm, BooksItemsVue },
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
    booksFromApi: []
  }),
  methods: {
    addBook (book) {
      this.books.push({ ...book })
    },
    removeBook (index) {
      this.booksFromApi.splice(index, 1)
      console.log('delete', index)
    },
    resetForm () {
      this.form.price = null
      this.form.title = ''
    },
    async retrieveBooks () {
      fetch('https://api.itbook.store/1.0/search/mongodb')
        .then(response => {
          console.log('Co tam jest w środku ?', response)
          response
            .json()
            .then(body => {
              console.log('body', body)
              this.booksFromApi = body.books
            })
        })
    }
  }
}
</script>
<template>
  <div class="app">
    <header>
      <h1 class="app__heading">Books<span>.app</span></h1>
    </header>
    <books-items-vue />
    <books-list @remove="removeBook" :books="books" />
    <books-list @remove="removeBook" :books="booksFromApi" />
    <!-- <books-length-msg :books="books"/> -->
    <books-length-msg :books="booksFromApi"/>
    <book-form @add="addBook"/>
    <button @click="retrieveBooks()"> Fetch Books </button>
    Books from api : {{ booksFromApi }}
  </div>
  <books-summary :books="books" />
  <hr>
  <books-items-vue />
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
