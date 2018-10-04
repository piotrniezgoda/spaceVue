<template>
  <div class="search-wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input id="search" type="text" name="search" v-model="searchValue" @input="handleInput">
      <ul>
      <li v-for="result in results" :key="result.data[0].nasa_id">
        <p>{{ result.data[0].description }}</p>
      </li>
    </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';
export default {
  name: 'Search',

  data() {
    return {
      searchValue: '',
      results: [],
    };
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
};
</script>

<style lang="scss" scoped>
  .search-wrapper {
    width: 100%;
    margin: 0;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 250px;

      input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid #000;
    }

      label {
        font-family: 'Montserrat', sans-serif;
    }

  }

</style>
