<template>
    <tr
      @click="$emit('rowClick', row)"
      v-observe-visibility="(isVisible, entry) => visibilityChangedHandler(isVisible, entry, row)">
      <table-cell v-for="column in visibleColumns" :row="row" :column="column" :key="column.id"/>
    </tr>
</template>

<script>
import Vue from 'vue'
import TableCell from './TableCell'
import VueObserveVisibility from '../directives/observe-visibility/index'
Vue.use(VueObserveVisibility)

export default {
  props: ['columns', 'row'],

  components: {
    TableCell
  },
  methods: {
    visibilityChangedHandler (isVisible, entry, row) {
      this.$emit('rowVisible', {row: row.data, isVisible})
    }
  },
  computed: {
    visibleColumns () {
      return this.columns.filter(column => !column.hidden)
    }
  }
}
</script>
