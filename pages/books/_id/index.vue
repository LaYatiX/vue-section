<template>
  <section class="single-book">
    <div class="title">
      <h1 v-show="shown.title" @dblclick="edit('title')">{{book.title}}</h1>
      <input v-show="!shown.title" type="text" v-model="book.title" @blur="reset" @keyup.enter="reset">
    </div>
    <div>
      <img :src="book.img" class="book-img" :alt="book.title">
    </div>
    <div class="author">
      <p v-show="shown.author" @dblclick="edit('author')">Autor: {{book.author}}</p>
      <input v-show="!shown.author" type="text" v-model="book.author" @blur="reset" @keyup.enter="reset">
    </div>
    <div class="description">
      <p v-show="shown.description" @dblclick="edit('description')">Opis: {{book.description}}</p>
      <input v-show="!shown.description" type="text" v-model="book.description" @blur="reset" @keyup.enter="reset">
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      shown: {},
      defaultShown: {
        title: true,
        author: true,
        description: true
      }
    }
  },
  created () {
    this.reset()
  },
  computed: {
    book () {
      return this.$store.state.books[this.$route.params.id - 1]
    }
  },
  methods: {
    edit (property) {
      this.shown[property] = false
    },
    reset () {
      this.shown = JSON.parse(JSON.stringify(this.defaultShown))
    }
  }
}
</script>
