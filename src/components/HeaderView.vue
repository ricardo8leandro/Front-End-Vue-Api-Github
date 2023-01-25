<template>
  <div class="header container">
    <img src="/img/vue.png" alt="Vue" />
    <p>Shaw and Partners Frontend</p>
  </div>
</template>

<script>
export default {
  name: 'HeaderView'
}
</script>


<style scoped>
.container {
  display: flex;
  align-items: center;
  background-color: #343a40;
  width: 100%;
  height:59px;
  color: #fff;
}

.container img {
  width: 30px;
  margin-left:30px;
  padding: 0 20px;
}

</style>
