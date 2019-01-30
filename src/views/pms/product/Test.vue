<template>
  <h1>{{msg}}</h1>
</template>

<script>
  export default {
    name: "test",
    data() {
      return {
        msg: "123456"
      }
    },
    created() {
      console.log(this.msg)
    }
  }
</script>

<style scoped>

</style>
