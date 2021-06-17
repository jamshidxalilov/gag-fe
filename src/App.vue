<template>
  <div id="app">
    <b-container>
      <b-card header="Test">
        <b-button variant="success" @click="loadItems()">Reload</b-button>
        <div class="text-center" v-if="loading">
          <b-spinner/>
        </div>
        <b-table class="mt-5" v-else :items="items"
                 :fields="fields"
        ></b-table>
      </b-card>
    </b-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      fields: [
        {key: "fname", text: "Ism"},
        {key: "lname", text: "Familiya"},
      ],
      items: []
    }
  },

  mounted() {
    this.loadItems()
  },
  methods: {
    loadItems() {
      this.loading = true
      fetch('/api/names/').then(r => r.json()).then(r => {
        this.items = r
        this.loading = false
      })
    }
  }
}
</script>

<style>

</style>
