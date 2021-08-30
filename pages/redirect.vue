<template>
  <div></div>
</template>

<script>
export default {
  name: 'Redirect',
  mounted() {
    console.log('redirected')
    this.$router.replace({ name: 'index' })
  },
}
</script>
