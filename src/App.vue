<template>
  <div id="app">
    <BSDataTable
      id="bs_table"
      :columns="columns"
      :rows="rows"
    ></BSDataTable>
  </div>
</template>

<script>
import BSDataTable from './components/BSDataTable'

export default {
  name: 'app',
  components: {
    BSDataTable
  },
  data () {
    return {
      columns: [{
        field: 'name',
        label: 'Nome'
      },
      {
        field: 'gender',
        label: 'Genero'
      },
      {
        field: 'age',
        label: 'Idade'
      }],
      rows: []
    }
  },
  mounted () {
    this.rows = require('assets/data.json')
  }
}
</script>
