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

      <div class="column is-3" v-for="book in latestBooks"
           v-bind:key="book.id">
        <div class="box">
          <figure class="image mb-4">
            <img :src="book.get_cover_art">
          </figure>

          <h3 class="is-size-4">{{book.name}}</h3>
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
      latestBooks: []
    }
  },

  components: {
  },

  mounted() {
    this.getLatestBooks()
  },

  methods: {
    getLatestBooks() {
      axios
        .get('/api/v1/latest-books')
        .then (response => {
          this.latestBooks = response.data
        })

      .catch(error => {
        console.log(error)
      })

    }
  }
}
</script>
