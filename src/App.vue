<template>
  <div class="app">
    <div class="search-wrapper">
      <Claim v-if="step === 0" />
      <SearchInput v-model="searchValue" :dark="step === 1" @input="handleInput"/>
      <HeroImage v-if="step === 0" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',

  data() {
    return {
      searchValue: '',
      results: [],
      loading: false,
      step: 0,
    };
  },

  components: {
    Claim,
    SearchInput,
    HeroImage,
  },

  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          console.log(this.results);
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),

  },
  props: {
    dark: {
      tpye: Boolean,
      default: false,
    },
  },

};
</script>


<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,500,800');
  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: 'Montserrat', sans-serif;
    font-size: 1rem;
    margin: 0;
    padding: 0;
    color: #fff;
  }

  .search-wrapper {
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .nav {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    padding: 15px 0;
  }

  .menu-link {
    color: #fff;
    text-decoration: none;
    margin: 0 25px;
    font-size: 1.1rem;
    text-transform: uppercase;
  }
</style>
