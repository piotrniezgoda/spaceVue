<template>
  <div class="app">
    <div :class="[{ flexStart: step === 1 }, 'wrapper']">
      <transition name="slide">
        <img src="./assets/logoSpacer.svg" class="app-logo" alt="" v-if="step === 1">
      </transition>
      <Claim v-if="step === 0" />
      <SearchInput v-model="searchValue" :dark="step === 1" @input="handleInput"/>
      <transition name="fade">
        <HeroImage v-if="step === 0" />
      </transition>
      <div class="results" v-if="results && !loading && step === 1">
        <item v-for="item in results" :item="item" :key="item.data[0].nasa_id" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';

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
    Item,
  },

  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
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

  .wrapper {
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;

    &.flexStart {
      justify-content: flex-start
    }
  }

  .app-logo {
    position: absolute;
    top: 40px;
    left: 50%;
    transform: translateX(-50%);
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

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top .5s ease;
}
.slide-enter, .slide-leave-to {
  margin-top: -50px;
}

.results {
  color: #000;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  width: 90%;
  margin-top: 80px;

  @media(min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
  }

}
</style>
