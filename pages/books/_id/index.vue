<template>
  <section class="single-book">
      <h1>{{book.title}}</h1>
    <div>
        <img :src="book.img" class="book-img" :alt="book.title">
    </div>
    <p class="book-title">Autor: {{book.author}}</p>
    <p class="book-description">Opis: {{book.description}}</p>
  </section>
</template>

<script>
export default {
  computed: {
    book () {
      return this.$store.state.books[this.$route.params.id - 1]
    }
  }
}
</script>
<style scoped>
  .single-book {
    background-color: #fafafa;
    width:30%;
    display: grid;
    grid-template-columns: auto;
    margin: 10px;
    border-radius: 5px;
    box-shadow: #AAAAAA 1px 3px;
  }
  .book-img {
    background-position: center;
    background-size: cover;
    width: 100%;
    height: 200px;
    border-radius: 5px;

  }
  .book-title{
    color: rgba(0,0,0,.9);
    padding-top: 10px;
    padding-left: 5px;
  }
  .book-description{
    color: rgba(0,0,0,.9);
    max-height: 100%;
    overflow: auto;
    padding-left:10px;
  }
</style>

