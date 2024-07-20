<template></template>

<script>
export default {
    beforeMount() {
    // const token = localStorage.getItem('token');
    // if (!token) {
      this.$router.push('/user/login');
    // }
  },
}
</script>

<style lang="scss"></style>