<template>
  <div class="app">
    <header>
      <h1 class="app__heading">Books<span>.app</span></h1>
      <!-- <button @click="retrieveBooks()">retrieve</button> -->
    </header>
    <books-items-vue />
    <books-list @remove="removeBook" :books="booksFromApi" />
    <books-length-msg :books="booksFromApi"/>
    <books-summary :books="booksFromApi" :books-from-api="books"/>
    <book-form @add="addBook"/>
  </div>
  <books-summary :books="booksFromApi" :books-from-api="books"/> <!-- :books to zmienna która jest stworzona w komponencie dziecka do której przypisujemy konkretną zmienna na której pracujemy-->
  <hr>
  <!-- <books-summary :best-seller-3="bestSelleByRating[0]" :best-seller-2="bestSelleByRating[1]" :best-seller-1="bestSelleByRating[2]" /> -->
  <books-items-vue />
</template>

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
    bestSellerArray: [
      {
        name: 'Kubus puchatek',
        rating: 10
      },
      {
        name: 'Dupadaupa',
        rating: 4
      },
      {
        name: 'to nie sa dyrjey',
        rating: 11
      }
    ],
    booksFromApi: []
  }),
  created () { // VUE lifecycle - wywołanie funkcji po wyrenderowaniu
    this.retrieveBooks()
  },
  // computed: {
  //   bestSelleByRating () {
  //     return this.bestSellerArray.sort((a, b) => a.rating - b.rating)
  //   }
  // },
  methods: {
    addBook (book) {
      this.books.push({ ...book })
    },
    removeBook (index) {
      this.booksFromApi.splice(index, 1)
      // this.books.splice(index, 1)
      // console.log('delete', index)
    },
    resetForm () {
      this.form.price = null
      this.form.title = ''
    },
    retrieveBooks () {
      fetch('https://api.itbook.store/1.0/search/mongodb')
        .then(response => {
          console.log('Co tam jest w środku ?', response)
          response
            .json()
            .then(body => {
              console.log('body', body)
              this.booksFromApi = body.books.slice(0, 3)
            })
        })
    }
  }
}
</script>
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
