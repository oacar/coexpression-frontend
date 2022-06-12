<template>
<b-container class="bv-example-row">
    <b-row>
        <b-col>
          <h3 style="color:coral">Query ORF info</h3>
            <b-table striped hover :items="orf_data" :fields="orf_data_fields">
          <template #cell(orf_name)="data">
            <a @click="gotoSGD(data.value)"
            target="_blank"     
            :class="computedClass(`${data.value}`)">
            {{data.value}}
            </a>
          </template>
      </b-table>
        </b-col>
        <b-col>
          <h3 style="color:coral">Query ORF coexpression table</h3>

            <b-table striped hover :items="coexpression_data" 
                id="my-table"
                :per-page="perPage"
                :current-page="currentPage">
              <template #cell(gene2)="data">
                <a @click="gotoSGD(data.value)"
                target="_blank"
                :class="computedClass(`${data.value}`)"
                >{{data.value}}</a>
              </template>
            </b-table>
          <p class="mt-3">Current Page: {{ currentPage }}</p>
          <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
      align="center"
    ></b-pagination>
        </b-col>
    </b-row>
    <b-row>
    <h1>Should add a network view of coexpression table</h1>
    </b-row>
</b-container>

</template>

<script>
  export default {
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
      }
    },
    computed: {
      rows() {
        return this.coexpression_data.length
      }
  },
    data() {
      return {
        perPage : 1,
        currentPage : 1,
        items: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' , idx:1 , foo:111},
          { age: 21, first_name: 'Larsen', last_name: 'Shaw' , idx:1},
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' , idx:2},
          { age: 38, first_name: 'Jami', last_name: 'Carney' , idx:1}
        ], 
        orf_data_fields : ['orf_name','length','start','end','strand'],
        orf_data: [
          {orf_name: 'YBR196C-A', length: '196', start: '1', end: '196', strand: '+',
          link : 'https://www.yeastgenome.org/locus/S000000680'},
        ],
        coexpression_data:[
          {gene1: 'YBR196C-A', gene2: 'YBR196C-B', coexpression: '.96'},
          {gene1: 'YBR196C-A', gene2: 'YBR196C', coexpression: '.95'},
          {gene1: 'YBR196C-A', gene2: 'YGR111C', coexpression: '.9'},
          {gene1: 'YBR196C-A', gene2: 'YHR112W-A', coexpression: '.86'},
          {gene1: 'YBR196C-A', gene2: 'foo', coexpression: '.76'},
        ]
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