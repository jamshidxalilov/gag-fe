<template>
  <div id="app">
    <b-container>
      <b-card header="Test">
        <b-table ref="tbl" class="mt-5" :items="loadItems" :fields="fields" />
      </b-card>

      <b-button @click="$refs.tbl.refresh()" :disabled="loading">
        <b-spinner v-if="loading" small/>
        Reload
      </b-button>
    </b-container>
  </div>
</template>

<script>

import moment from 'moment'
export default {
  data() {
    return {
      loading: false,
      fields: [
        {key: "fname", label: "Ism"},
        {key: "lname", label: "Familiya"},
        {key: "qs", label: "Qo'shilgan sanasi", formatter(v){
          return moment(v).format("DD.MM.YYYY HH:mm")
          }},
      ],
    }
  },

  mounted() {
    this.loadItems()
  },
  methods: {
    async loadItems() {
      this.loading = true
      let r = await this.$axios.get('names/')
      this.loading = false
      return r.data
    }
  }
}
</script>

<style>

</style>
