<template>
<div class="result">
    <div v-if="loading" class="loading">Loading...</div>

    <div v-if="error" class="error">{{ error }}</div>

    <div v-if="result" class="content">
    <h2>{{result.orf_id}}</h2>
    <orf-table :coexpression="result.coexpression" :properties="result.orf_properties" :orf_id="result.orf_id" />
    <!-- <p>{{ post.body }}</p> -->
    </div>
</div>
</template>

<script>
import axios from 'axios'
import OrfTable from '@/components/Table.vue' 
export default {
  data() {
    return {
      loading: false,
      result: null,
      error: null,
    }
  },
  components: {
   OrfTable 
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
        const path = 'http://localhost:5000/orf_name/'+orfName;
        console.log(path)
        axios.get(path)
        .then(response => {
            this.loading = false
            console.log(response.data)
            this.result = response.data
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