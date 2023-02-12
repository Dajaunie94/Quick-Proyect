<template>
  <div class="dashboard">
  	 <Header/>
       <div class="container">         	
           <div class="overflow-auto">					   
						    <b-table
						      id="my-table"
						      :items="listAthlete"
						      :per-page="elements"
						      :current-page="currentPage"
						      small
						      class="table-dark"
						    ></b-table>
						    <b-pagination
						      v-model="currentPage"
						      :total-rows="rows"
						      :per-page="elements"
						      aria-controls="my-table"
						    ></b-pagination>
				    </div>
      </div>
     <Footer/>
  </div>
</template>

<script>
// @ is an alias to /src

import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
  name: 'Dashboard',
  data(){
    return {
    	listAthlete:[],
    	elements:10,
    	currentPage:1


    }
  },
  components: {
    Header,
    Footer
  },
  mounted:function(){

  	let direccion = "https://raw.githubusercontent.com/ag-grid/ag-grid/master/grid-packages/ag-grid-docs/src/olympicWinners.json";	
  	axios.get(direccion).then(data=>{
  		
  		this.listAthlete= data.data 	
  	})
  		
  }, 
  computed: {
      rows() {
        return this.listAthlete.length
      }
    }
}
</script>

<style lang="stylus" scoped>

</style>