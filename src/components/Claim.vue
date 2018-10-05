<template>
  <div class="claim-wrapper">
    <h1 class="claim">spacer</h1>
    <p class="subclaim">discover places you never even heard of.</p>
    <p class="subclaim">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
  .claim-wrapper {
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .claim {
    margin: 0 0 25px;
    font-size: 4rem;
    text-transform: uppercase;
  }

  .subclaim {
    font-size: 0.9rem;
  }
</style>
