<template>
  <div id="main-banner">
    <h1>Monte sua Quadrada</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/public/img/banner3.png");
  background-position: 0 -180px;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

#main-banner h1{
    text-transform: uppercase;
    color: #FFF;
    text-align: center;
    font-size: 30px;
    padding: 20px;
    background-color: #222;
}
</style>
