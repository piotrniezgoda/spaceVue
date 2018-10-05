<template>
  <div class="searchInput-wrapper">
      <input id="search" type="text" name="search" v-model="searchValue" @input="handleInput">
    </div>
</template>

<script>
const API = 'https://images-api.nasa.gov/search';
import axios from 'axios';
import debounce from 'lodash.debounce';
export default {
  name: 'SearchInput',
  data() {
    return {
      searchValue: '',
      results: [],
    }
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function() {
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
}
</script>

<style lang="scss" scoped>
.searchInput-wrapper {
    display: flex;
    flex-direction: column;
    width: 250px;
    margin: 40px 0 0 0;

      input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid #fff;
        background: transparent;
    }

      label {
        font-family: 'Montserrat', sans-serif;
    }

  }
</style>
