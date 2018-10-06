<template>
  <div class="hero-image"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style lang="scss" scoped>
  .hero-image {
    background: url('../assets/appBg.jpg');
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 80% 80%;
    position: fixed;
    width: 100%;
    min-height: 100vh;
    top: 0;
    left: 0;
    z-index: -1;

    &::after {
      position: absolute;
      content: '';
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      background: rgba(0,0,0,0.20);
    }

    @media(min-width: 1024px) {
      background-position: 0% 100%;
    }
  }
</style>
