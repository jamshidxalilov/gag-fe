<template>
  <div id="app">
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-container>
        <b-navbar-brand :to="{name: 'home'}">Vue</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item :to="{name: 'home'}" :active="$route.name == 'home'">Home</b-nav-item>
            <b-nav-item :to="{name: 'about', params: {id: 55}}" :active="$route.name == 'about'">About</b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </b-container>
    </b-navbar>
<!--    <b-container class="mt-5">-->
<!--      <b-card header="Test">-->
<!--        <b-table ref="tbl" class="mt-5" :items="loadItems" :fields="fields" />-->
<!--      </b-card>-->

<!--      <b-button @click="$refs.tbl.refresh()" :disabled="loading">-->
<!--        <b-spinner v-if="loading" small/>-->
<!--        Reload-->
<!--      </b-button>-->


<!--    </b-container>-->
    <b-container>
      <router-view />
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
