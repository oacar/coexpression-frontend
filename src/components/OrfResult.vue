<template>
<div class="result">
    <div v-if="loading" class="loading">Loading...</div>

    <div v-if="error" class="error">{{ error }}</div>

    <div v-if="post" class="content">
    <h2>{{post}}</h2>
    <!-- <p>{{ post.body }}</p> -->
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      loading: false,
      post: null,
      error: null,
    }
  },
  created() {
    // watch the params of the route to fetch the data again
    this.$watch(
      () => this.$route.params,
      () => {
        this.fetchData()
      },
      // fetch the data when the view is created and the data is
      // already being observed
      { immediate: true }
    )
  },
  methods: {
    fetchData() {
      this.error = this.post = null
      this.loading = true
      // replace `getPost` with your data fetching util / API wrapper
      var orfName = this.$route.params.orfName
        const path = 'http://localhost:5000/'+orfName;
        console.log(path)
        axios.get(path)
        .then(response => {
            this.loading = false
            console.log(response.data)
            this.post = response.data
        })
        .catch(error => {
            this.loading = false
            console.log(error)
            this.error = error
        })
    },
  },
}
</script>

<style>

</style>