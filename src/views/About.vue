<template>
  <div class="about">
    <h1>This is an about page</h1>

    <b-button @click="goBack">Go home</b-button>
  </div>
</template>


<script>
export default {
  methods: {
    goBack() {
      this.$router.push({name: 'home'})
    }
  },
  mounted() {
    alert(this.$route.params.id)
  }
}
</script>