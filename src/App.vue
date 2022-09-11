<template>
  <div id="app">
    <header>
      <h1>Books<span>.app</span></h1>
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
<style>
  li {
    padding: 5px;
  };
</style>
