<template>
<transition
  enter-active-class="animate__animated animate__fadeInDown"
  leave-active-class="animate__animated animate__fadeOutUp"
>
  <div id="main-banner">
      <h1 class="animate__animated animate__bounce">Faça o seu hamburguer!</h1>
  </div>
</transition>
  
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/img/banner-1.jpeg");
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

    
  animation: bounce; /* referring directly to the animation's @keyframe declaration */
  animation-duration: 2s; /* don't forget to set a duration! */
}

@media screen and (min-width: 1400px)  {
  h1 {
    font-size:5px;
  }
}

</style>
