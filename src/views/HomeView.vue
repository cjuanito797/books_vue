<template>
  <div class="home">
    <section class="here is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Welcome to the Book Store
        </p>
        <p class="subtitle">
          Home of the best books available.
        </p>
      </div>
    </section>

    <div class="column is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest Books</h2>
      </div>
      <div class="columns">
        <div class="is-one-fifth column" v-for="book in latestBooks"
             v-bind:key="book.id">
          <div class="box">
            <figure class="image mb-4">
              <img :src="book.get_cover_art">
            </figure>
            <div class="columns is-centered">
              <h3 class="is-size-4">{{ book.name }}</h3>
            </div>
            <div class="is-centered columns">
              <button v-on:click="addToCart(book)" class="is-primary button is-small">Add to cart
              </button>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'HomeView',
  data() {
    return {
      latestBooks: [],
      cartBooks: {}
    }
  },

  components: {},

  mounted() {
    this.getLatestBooks()
    this.cartBooks = this.$store.state.books
  },

  methods: {
    getLatestBooks() {
      axios
          .get('/api/v1/latest-books')
          .then(response => {
            this.latestBooks = response.data
          })

          .catch(error => {
            console.log(error)
          })
    },
    addToCart(book) {
      if (this.cartBooks.hasOwnProperty(book.id)) {
        this.cartBooks[book.id].count++
      } else {
        this.cartBooks[book.id] = {
          'book': book,
          'count': 1
        }
      }
      this.$store.state.books = this.cartBooks
      console.log(this.$store.state.books)
      alert("added successfully")

    }
  }

}
</script>