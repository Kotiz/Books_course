<template>
  <div id="app">
    <header>
      <h1>Books<span>.app</span></h1>
    </header>
    <ul>
      <li v-for="(book, index) in books" :key="index">
        {{ book.title }}, {{ book.price }}$
        <button @click="removeBook">Delete book</button>
      </li>
    </ul>
    <p v-show="!books.length">No books...</p>
    <form @submit.prevent="handleSubmit">
      <label>
        Title:
        <input v-model="form.title" type="text" name="title">{{ form.title }}
      </label>
      <label>
        Price:
        <input v-model="form.price" type="number" name="price">{{ form.price }}
      </label>
      <button>Add book </button>
    </form>
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
      console.log('delete')
    }
  },
  handleSubmit () {
    this.books.push({ ...this.form })
    console.log('submit')
  }
}
</script>
<style>
  li {
    padding: 5px;
  };
</style>
