<template>
<div class="master-grid">
      <h1 class="header">Książki</h1>
  <div class="books-container">
        <Book
            v-for="book in $store.state.books"
            :key="book.id"
            :img="book.img"
            :title="book.title"
            :description="book.description"
            :id="book.id"
        />
  </div>
</div>

</template>

<script>
import Book from '@/components/Book'
import 'isomorphic-fetch'
export default {
  components: {
    Book
  },
  methods: {
    transform (bookItem, index) {
      const book = bookItem.volumeInfo
      return {
        id: index + 1,
        title: book.title,
        description: book.description,
        img: book.imageLinks ? book.imageLinks.thumbnail : 'http://books.google.com/books/content?id=PXa2bby0oQ0C&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api',
        author: book.authors ? book.authors[0] : 'Unknown'
      }
    },
    getBooks () {
      const query = 'knit'
      return fetch(`https://www.googleapis.com/books/v1/volumes?q=${encodeURIComponent(query)}`)
        .then((response) => {
          return response.json()
        })
        .then((result) => {
          if (this.$store.state.books.length === 0) {
            this.$store.state.books = result.items ? result.items.map(this.transform) : []
          }
        })
    }
  },
  created () {
    this.getBooks()
  }
}
</script>


<style scoped>
  .master-grid{
    display:grid;
    grid-template-rows:200px repeat(10, 300px);;
    background-color: #EEEEEE;

  }
  .header{
    font-size: 300%;
    text-align: center;
    padding-top: 5%;
    /*grid-row-start: 1;
    grid-row-end: 5;*/

  }
  .books-container {
    display: grid;
    grid-auto-flow: dense;
    list-style: none;
    grid-template-columns: 1fr  1fr  1fr 1fr 1fr;
    grid-column-gap: 1%;
    grid-row-gap: 1%;
    align-items:stretch;
  }
  @media only screen and (max-width: 1029px) {
    .books-container {
      grid-column-gap: 2%;
      grid-template-columns: 2fr  2fr;
    }
  }
</style>

