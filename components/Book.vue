<template>
    <nuxt-link :to="'/books/' + id">
        <div class="single-book">
          <div class="book-img" :style="{backgroundImage: 'url('+ img +')'}"></div>
            <h2 class="book-title">{{title}}</h2>
            <p>{{author}}</p>
            <div class="book-description">{{description}}</div>
        </div>
    </nuxt-link>
</template>

<script>
export default {
  props: ['title', 'author', 'description', 'img', 'id']
}
</script>
<style scoped>
  .single-book {
    background-color: #fafafa;
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
    overflow: auto;
    padding-left:10px;

  }
</style>
