<template>
  <div>
    <h1>{{ msg }}, сегодня {{ getTime }}</h1>
  </div>
</template>

<script>
export default {
  name: 'AppHead',
  props: {
    msg: String
  },
  computed: {
    getTime() {
      const today = new Date();
      const day = today.getDate();
      let month = today.getMonth() + 1;
      if (month.toString().length === 1) {
        month = '0' + month;
      }
      return `${day}.${month}`;
    }
  }
}
</script>

<style scoped>

</style>
