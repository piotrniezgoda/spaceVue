<template>
    <div :class="[{ flexStart: step === 1 }, 'wrapper']">
      <transition name="slide">
        <img src="./assets/logoSpacer.svg" class="app-logo" alt="" v-if="step === 1">
      </transition>
      <Claim v-if="step === 0" />
      <SearchInput
      v-model="searchValue"
      :dark="step === 1"
      @input="handleInput"/>
      <transition name="fade">
        <HeroImage v-if="step === 0" />
      </transition>
      <div class="results" v-if="results && !loading && step === 1">
        <item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)" />
      </div>
      <div class="lds-roller" v-if="step === 1 && loading">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
      <Modal :item="modalItem" v-if="modalOpen" @closeModal="modalOpen = false" />
    </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',

  data() {
    return {
      searchValue: '',
      results: [],
      loading: false,
      modalOpen: false,
      step: 0,
      modalItem: null,
    };
  },

  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
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

    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
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
  grid-gap: 10px;
  width: 100%;
  margin-top: 80px;

  @media(min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px;
    width: 90%;
  }
}

.lds-roller {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
  margin-top: 40px;
}
.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 32px 32px;
}
.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: rgb(71, 71, 71);
  margin: -3px 0 0 -3px;
}
.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
  top: 50px;
  left: 50px;
}
.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
  top: 54px;
  left: 45px;
}
.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
  top: 57px;
  left: 39px;
}
.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
  top: 58px;
  left: 32px;
}
.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
  top: 57px;
  left: 25px;
}
.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
  top: 54px;
  left: 19px;
}
.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
  top: 50px;
  left: 14px;
}
.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
  top: 45px;
  left: 10px;
}
@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
