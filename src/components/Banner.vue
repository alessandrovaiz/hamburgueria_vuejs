<template>
  <div id="main-banner">
      <h1>Faça o seu hamburguer!</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/img/banner-1.jpeg");
  background-position: 0 -450px;
  background-size: cover;
  height:500px;
  width:100%;
  display:flex;
  align-items:center;
  justify-content:flex-start;
}

#main-banner h1 {
    color: #fff;
    text-align:center;
    font-size:60px;
    background-color: #222;
    padding: 20px 40px;
}

</style>
