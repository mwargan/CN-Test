<template>
  <div class="result card flex-columns">
    <div class="column">
      <img src="https://blog.mmediagroup.fr/wp-content/uploads/2020/07/ZJfzZw1zVBT0pNplfkgM5lug86AYM7K1yPLCeV45.jpeg" alt="">
    </div>
    <div class="column" style="flex:1;">
      <div class="title">{{title}}</div>
      <div class="date">{{parsedDate}}</div>
      <p>{{body}}</p>
    </div>
    <div class="column column-vertical-center">
      <div class="rating">{{parsedRating}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Result',
  props: {
    body: String,
    title: String,
    date: Number,
    rating: Number
  },
  computed: {
    parsedDate () {
      const resultDate = new Date(this.date)
      const dd = resultDate.getDate()
      const mm = resultDate.getMonth() + 1
      const yyyy = resultDate.getFullYear()
      return dd + '/' + mm + '/' + yyyy
    },
    parsedRating () {
      return Math.round(this.rating / 10)
    }
  }
}
</script>
