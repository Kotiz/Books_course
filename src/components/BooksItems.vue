<script>
export default {
  name: 'booksItems',
  data: () => ({
    booksApi: [],
    methods: {
      getBooks () {
        fetch('https://api.itbook.store/1.0/search/mongodb')
          .then(response => response.json())
          .then(data => (this.booksApi = data))
      }
    }
  }
  )
}
</script>
<template>
  <div v-for="book in booksApi" :key="book">
    <span>{{ booksApi.books }}</span>
    <button @click="getBooks">Show Books</button>
  </div>
</template>
