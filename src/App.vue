<script>
import BooksList from './components/BooksList.vue'
import BooksLengthMsg from './components/BooksLengthMsg.vue'
import booksSummary from './components/BookSummary.vue'
// import booksItem from './components/BooksItems.vue'
export default {
  components: { BooksList, BooksLengthMsg, booksSummary },
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
    form: {
      title: '',
      price: 0
    }
  }),
  methods: {
    removeBook (index) {
      this.books.splice(index, 1)
      console.log('delete', index)
    },
    handleSubmit () {
      const newBook = { ...this.form }
      this.books.push(newBook)
      this.resetForm()
    },
    resetForm () {
      this.form.price = null
      this.form.title = ''
    }
  }
}
</script>
<template>
  <div class="app">
    <header>
      <h1 class="app__heading">Books<span>.app</span></h1>
    </header>
    <books-list @remove="removeBook" :books="books" />
    <books-length-msg :books="books"/>
    <form @submit.prevent="handleSubmit">
      <label>
        Title:
        <input v-model="form.title" type="text" name="title">
      </label>
      <label>
        Price:
        <input v-model="form.price" type="number" name="price">
      </label>
      <button type="submit">Add book</button>
    </form>
  </div>
  <books-summary :books="books" />
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
