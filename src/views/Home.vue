<template>
  <div class="content">
    <div class="grid-columns">
      <div class="grid-column">
        <div class="filters card">
          <div class="card-heading">Filter results</div>
          <label>Name (contains)
            <input type="text" name="" value="" v-model="searchTerm">
          </label>
          <label>Minimum score
            <input type="number" min="1" max="10" v-model="minimumScore">
          </label>
          <label for="orderBy">Order by</label>
          <div class="order-by-input-group">
              <button v-bind:class="{ flipped: orderByAscending === false }" @click="orderByAscending = !orderByAscending">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-up" viewBox="0 0 16 16">
                  <path fill-rule="evenodd" d="M8 15a.5.5 0 0 0 .5-.5V2.707l3.146 3.147a.5.5 0 0 0 .708-.708l-4-4a.5.5 0 0 0-.708 0l-4 4a.5.5 0 1 0 .708.708L7.5 2.707V14.5a.5.5 0 0 0 .5.5z" />
                </svg>
              </button>
              <select name="orderBy" id="orderBy" v-model="orderBy">
                <option value="first_release_date">Release date</option>
                <option value="rating" selected>Score</option>
                <option value="name">Name</option>
              </select>
          </div>
          <button type="button" v-if="shouldShowClearButton" @click="clearFilters()">Clear</button>
        </div>
      </div>
      <div class="grid-column results">
        <template v-if="filteredAndOrderedResults.length > 0">
          <result v-for="result in filteredAndOrderedResults" :rating="result.rating" :title="result.name" :date="result.first_release_date" :body="result.summary" :key="result.id"></result>
        </template>
        <div v-else-if="loading" class="result card">Loading....</div>
        <div v-else class="result card">No results found</div>
      </div>
    </div>
  </div>
</template>
<script>
import Result from '../components/Result.vue'
import axios from 'axios'

export default {
  name: 'App',

  components: {
    Result
  },

  data () {
    return {
      results: [],
      searchTerm: '',
      minimumScore: 1,
      orderBy: 'rating',
      orderByAscending: false,
      loading: true
    }
  },

  mounted () {
    setTimeout(() => {
      this.getData()
    }, 2000)
  },

  computed: {
    filteredAndOrderedResults () {
      if (this.results.length === 0) {
        return []
      }

      const results = this.results.filter(result => result.name.toLowerCase().includes(this.searchTerm.toLowerCase()) && Math.round(result.rating / 10) >= this.minimumScore)

      return results.sort((a, b) => {
        if (this.orderByAscending) {
          return a[this.orderBy] > b[this.orderBy] ? 1 : -1
        } else {
          return a[this.orderBy] < b[this.orderBy] ? 1 : -1
        }
      })
    },
    shouldShowClearButton () {
      if (this.minimumScore > 1 || this.searchTerm) {
        return true
      }
      return false
    }
  },

  methods: {
    async getData () {
      try {
        this.loading = true
        const fetchedData = await axios.get('https://public.connectnow.org.uk/applicant-test/')
        this.results = fetchedData.data
      } catch (error) {
        alert(error)
      }
      this.loading = false
    },
    clearFilters () {
      this.searchTerm = ''
      this.minimumScore = 1
    }
  }

}

</script>
<style lang="scss" scoped>
</style>
