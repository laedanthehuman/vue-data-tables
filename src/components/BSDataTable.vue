<template>
<div class="table-responsive">
  <table :id="id" :class="`table ${classes}`">
    <thead>
      <tr>
        <slot name="extra-header-left"></slot>
        <th v-for="column in columns" :key="column.field" v-text="column.label"></th>
        <slot name="extra-header-rigth"></slot>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, indexRow) in rows" :key="indexRow">
        <slot name="extra-column-left"></slot>
        <td v-for="column in columns" :key="column.field" v-text="row[column.field]"></td>
        <slot name="extra-column-rigth"></slot>
      </tr>
    </tbody>
  </table>
  <nav aria-label="...">
    <ul class="pagination">
      <li :class="isActualPage" v-for="(page, index) in pages" :key="index" v-text="page"></li>
    </ul>
  </nav>
</div>
</template>

<script>
export default {
  name: 'BS-DATA-TABLE',
  computed: {
    isActualPage () {
      return this.pagination.actualPage
    }
    rowsTable () {
      const rowsTable = Array.from(this.rows)
      const actualPage = this.pagination.actualPage
      const previusPage = actualPage - 1
      const itensPerPages = this.pagination.pageSize
      const prevPage = actualPage*itensPerPages
      const nexPage = previusPage*itensPerPages

      if ( this.totalRows < itensPerPages) return this.rows

      return rowsTable.filter((item,index) => index <prevPage  && index >=nexPage )
    },
    totalRows () {
      this.rows.length
    },
    pages () {
      return Array(this.pagination.pageSize).fill('').map((i, index) => i = index)
    }
  }
  data () {
    return {
      pagination: {},

    }
  },
  created () {
    this.pagination = Object.assign({}, {
        pageSize: 20,
        pageSizes: [20, 50, 100],
        currentPage: 1
      }, this.paginationDef)
  }
  props: {
    columns: {
      type: Array,
      required: true
    },
    rows: {
      type: Array,
      required: true
    },
    id: {
      type: String,
      default: ''
    },
    classes: {
      type: String,
      default: ''
    },
    paginationDef: {
      type: Object,
      default: () => {}
    }
  }
}
</script>

<style lang="sass" src="assets/sass/app.scss">
</style>
