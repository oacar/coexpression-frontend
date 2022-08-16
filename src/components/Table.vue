<template>
    <b-container class="bv-example-row">
            <h3 style="color:coral">{{table_name}}</h3>
                <b-table striped hover :items="table_data" :fields="table_fields">
            <template #cell(orf_name)="data">
                <a @click="gotoSGD(data.value)"
                target="_blank"     
                :class="computedClass(`${data.value}`)">
                {{data.value}}
                </a>
            </template>
            <template #cell(cluster_id)="data">
                <a @click="getClusterProperty(data.value)"
                target="_blank"     
                >
                {{data.value}}
                </a>
            </template>
        </b-table>
    </b-container>

</template>

<script>

export default {
    name: "OrfTable",
    props: {
      'orf_id': Number,
      'table_data': Array,
       'table_name': String,
       'table_fields': Array,},

    methods:{
      gotoSGD(orf_name){
        if(orf_name.includes("Y")){
          window.open(`https://www.yeastgenome.org/locus/${orf_name}`)
      }else{
        null 
      }
    },

      computedClass(orf_name) {
        let className = 'unannotated';
        if (orf_name.includes("Y")) {
          className = 'annotated';
        }
        return className;
      },
      getClusterProperty(cluster_id){
        // let cluster_property = this.table_data.find(function(item){
        //   return item.cluster_id == cluster_id
        // })
        // return cluster_property
        console.log(cluster_id)
      }
    } ,
    data() {
      return {
        rows : 5,
        perPage : 5,
        currentPage : 1,
      }
    }
}
</script>

<style scoped>
a { text-decoration: none;
    color: black; 
    font-weight: bold; }

.annotated {
  color: #006600;
}
.unannotated {
	color:grey;
	text-decoration:none;
	cursor:default;
}

</style>