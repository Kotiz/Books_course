<template>
  <div id="app">
    <header>
      <h1>Books<span>.app</span></h1>
    </header>
    <ul>
      <li v-for="(book, index) in books" :key="index">
        {{ book.title }}, {{ book.price }}$
        <button @click="removeBook(index)">Delete book</button>
      </li>
    </ul>
    <form @submit.prevent="handleSubmit">
      <label>
        Title:
        <input v-model="form.title" type="text" name="title">
      </label>
      <label>
        Price:
        <input v-model="form.price" type="number" name="price">
      </label>
      <button type="submit">Add book 2 </button>
    </form>
    <p v-if="books.length < 1">Get some books !</p>
    <p v-else-if="books.length > 5 "> No. of books : {{ books.length }}</p>
    <p v-else-if="books.length <= 5 && books.length > 1 ">Not to many of them...</p>
    <p v-else-if="books.length == 1 ">One single book</p>
  </div>
</template>
<script>
export default {
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
      }
    ],
    form: {
      title: '',
      price: null
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
