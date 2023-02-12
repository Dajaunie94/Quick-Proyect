<template>
  <div class="characteristics">
    <Header/>
    <div class="container">
  <b-container fluid>
    
    <!-- Main table element -->
    <b-table
      :items="items"
      :fields="fields"
      :current-page="currentPage"
      :per-page="perPage"            
      stacked="md"
      show-empty
      small
      icon="x-circle"
    >
      <template #cell(name)="row">
        {{ row.value.first }} {{ row.value.last }} 
      </template>

      <template #cell(actions)="row">
        <b-button  size="sm" @click="info(row.item, row.index, $event.target)" class="mr-1" >
          Info Medalla
        </b-button>
      </template>

      <template #row-details="row">
        <b-card>
          <ul>
            <li v-for="(value, key) in row.item" :key="key">{{ key }}: {{ value }}</li>
          </ul>
        </b-card>
      </template>
    </b-table>

    <!-- Info modal -->
    <b-modal :id="infoModal.id" :title="infoModal.title" ok-only @hide="resetInfoModal">
      <pre>{{ infoModal.content }}</pre>
      <br>
    </b-modal>
  </b-container>
  </div>
  <Footer/>
</div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
  export default {
    data() {
      return {
        listAthlete:[],
        items: [
          { total: 120, icon: '@/assets/gold.png', name: { first: 'Medalla ', last: 'Oro' },content:'Una medalla de Oro es una medalla que se otorga al Primer clasificado de diversas competiciones como los Juegos Olímpicos.' },
          { total: 320, icon: '@/assets/silver.png', name: { first: 'Medalla ', last: 'PLata' },content:'Una medalla de Plata es una medalla que se otorga al Segundo clasificado de diversas competiciones como los Juegos Olímpicos.' },
          { total: 552, icon: '@/assets/bronza.png', name: { first: 'Medalla', last: 'Bronce'},content:'Una medalla de bronce es una medalla que se otorga al tercer clasificado de diversas competiciones como los Juegos Olímpicos.' },
          
        ],
        fields: [
          { key: 'icon', label: 'Logo', sortable: true, sortDirection: 'desc' },
          { key: 'name', label: 'Medalla', sortable: true, class: 'text-center' },
          {
            key: 'total',
            label: 'Total',                    
          },
          { key: 'actions', label: 'Actions' }
        ],
        totalRows: 1,
        currentPage: 1,
        perPage: 5,
        pageOptions: [5, 10, 15, { value: 100, text: "Show a lot" }],
        sortBy: '',
        sortDesc: false,
        sortDirection: 'asc',
        filter: null,
        filterOn: [],
        infoModal: {
          id: 'info-modal',
          title: '',
          content: ''
        }
      }
    },
    components: {
    Header,
    Footer
  },
    computed: {
      sortOptions() {
        // Create an options list from our fields
        return this.fields
          .filter(f => f.sortable)
          .map(f => {
            return { text: f.label, value: f.key }
          })
      }
    },
    mounted() {
      // Set the initial number of items
      this.totalRows = this.items.length
      let direccion = "https://raw.githubusercontent.com/ag-grid/ag-grid/master/grid-packages/ag-grid-docs/src/olympicWinners.json";  
    axios.get(direccion).then(data=>{
      this.listAthlete= data.data 

    })
    },
    methods: {
      info(item, index, button) {
        this.infoModal.title = `Row index: ${index}`
        this.infoModal.content = JSON.stringify(item.content, null, 2)
        console.log(this.infoModal.content);
        this.$root.$emit('bv::show::modal', this.infoModal.id, button)
      },
      resetInfoModal() {
        this.infoModal.title = ''
        this.infoModal.content = ''
      },
      
    }
  }
</script>