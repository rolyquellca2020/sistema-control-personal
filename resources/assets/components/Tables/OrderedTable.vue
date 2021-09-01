<template>
  <div>
    <md-table v-model="eventsError" :table-header-color="tableHeaderColor">
      <md-table-row slot="md-table-row" slot-scope="{ item }">
        <md-table-cell md-label="#">{{ item.id }}</md-table-cell>
        <md-table-cell md-label="Evento">{{ item.evento }}</md-table-cell>
        <md-table-cell md-label="Fecha - Hora">{{ item.created_at }}</md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>

<script>
export default {
  name: 'ordered-table',
  props: {
    tableHeaderColor: {
      type: String,
      default: ''
    }
  },
  created(){
    this.getFiveLastErrors();
  },
  data () {
    return {
      selected: [],
      eventsError: []
    }
  },
  methods:{
    getFiveLastErrors(){
      axios.get('/marks/errors/five').then(response => { this.eventsError = response.data; }).catch(errors => { console.log(errors); })
    },

    actualizar: function () {
      setInterval(this.getFiveLastErrors, 10000);
   }
  },
  mounted(){
    this.actualizar()
  }
};
</script>
