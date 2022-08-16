<template>
<div class="result">
    <div v-if="loading" class="loading">Loading...</div>

    <div v-if="error" class="error">{{ error }}</div>

    <div v-if="result" class="content">
    <!-- <h2>{{result.orf_id}}</h2> -->
    <b-container>
    <orf-table table_name="ORF Info" :table_data="[orf_info]"  :orf_id="result.orf_id" />
    <orf-table table_name="Coexpression Info" :table_data="[result.coexpression]"  :orf_id="result.orf_id" />
    <div v-if="Object.keys(result.cluster).length > 0">
   <orf-table table_name="Cluster Info" :table_data="[result.cluster]"  :orf_id="result.orf_id" /> 
   <div v-if="Object.keys(result.cluster_go).length > 0">
   <orf-table table_name="Cluster GO enrichments" :table_data="[result.cluster_go]"  :orf_id="result.orf_id" /> 
</div>
    </div> 
    </b-container>
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
  computed: {
    orf_info() {
      var size = Object.keys(this.result.cluster).length
      if (size> 0) {
        let orf_info = Object.assign(this.result.orf_properties, this.result.network_properties)
        return orf_info
      }
      return this.result.orf_properties
    },
    orf_property_fields() {
      let fields = ['orf_name',"cluster_id", 'orf_length','orf_start','orf_end','orf_strand',"orf_sequence"]
      return fields 
    },
    coexpression_fields() {
      let fields = ['Orf1','Orf2','rho','pearson_r', 'spearman_r']
      return fields 
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