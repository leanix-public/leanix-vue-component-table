<template>
  <div id="app">
    <div class="title">{{info.name}} v{{info.version}}</div>
    <div class="subtitle">{{info.description}}</div>
    <a :href="info.repository.url">{{info.repository.url}}</a>
    <table-component
      @row-click="handleRowClick"
      @row-visible="handleRowVisible"
      @last-row="handleLastRowChanged"
      :data="[
          { firstName: 'John', lastName: 'Lennon', instrument: 'Guitar', birthday: '04/10/1940', songs: 1 },
          { firstName: 'Paul', lastName: 'McCartney', instrument: 'Bass', birthday: '18/06/1942', songs: 7 },
          { firstName: 'George', lastName: 'Harrison', instrument: 'Guitar', birthday: '25/02/1943', songs: 10 },
          { firstName: 'Ringo', lastName: 'Starr', instrument: 'Drums', birthday: '07/07/1940', songs: 20 },
          { firstName: 'John', lastName: 'Lennon', instrument: 'Guitar', birthday: '04/10/1940', songs: 1 },
      ]"
      sort-by="songs"
      sort-order="asc"
      >
      <table-column show="firstName" label="First name"></table-column>
      <table-column show="lastName" label="Last name"></table-column>
      <table-column show="instrument" label="Instrument"></table-column>
      <table-column show="songs" label="Songs" data-type="numeric"></table-column>
      <table-column show="birthday" label="Birthday" data-type="date:DD/MM/YYYY"></table-column>
      <table-column :sortable="false" :filterable="false">
        <template slot-scope="artist">
          <a :href="'#' + artist.firstName.toLowerCase()">
            Edit
          </a>
        </template>
      </table-column>
      <template slot="tfoot" slot-scope="{ rows }">
        <tr>
          <th>&nbsp;</th>
          <th>&nbsp;</th>
          <th>Total Songs:</th>
          <th>{{ rows.reduce((sum, value) => { return sum + value.data.songs; }, 0) }}</th>
          <th>&nbsp;</th>
          <th>&nbsp;</th>
        </tr>
      </template>
    </table-component>
    <div class="event-box">
      <span class="title">Events</span>
      <span class="msg">{{eventMsg}}</span>
    </div>
  </div>
</template>

<script>
import _info from '../../package.json'
import { TableColumn, TableComponent } from '../../src'
export default {
  name: 'App',
  components: { TableColumn, TableComponent },
  data () {
    return {
      info: _info,
      eventMsg: ''
    }
  },
  methods: {
    handleRowClick (event) {
      this.eventMsg = `row-click => ${event.data.firstName}`
    },
    handleRowVisible (row) {
      // this.eventMsg = row
    },
    handleLastRowChanged (row) {
      // this.eventMsg = row
    }
  }
}
</script>

<style lang="stylus">
@import '~@/stylus/table-component'

#app
  font-family: Helvetica Neue,Helvetica,Arial,sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
  padding 3rem
  cursor default

.title
  font-size 2.5rem
  margin-bottom 1rem
.subtitle
  font-size 1.5rem
  margin-bottom 1rem
.event-box
  display flex
  flex-flow column
  .title
    font-size 1.3rem
    padding 1rem
    font-weight bold
  .msg
    font-size 0.9rem

</style>
