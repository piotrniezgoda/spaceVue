<template>
  <div class="search-wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
// eslint-disable-next-line
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';


export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
  },

  methods: {
  },
}
</script>

<style lang="scss" scoped>
  .search-wrapper {
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: url('../assets/appBg.jpg');
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 80% 0%;
  }

</style>
