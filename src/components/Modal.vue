<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="photo" alt="">
      </div>
      <div class="description">
        <h2 class="title">{{ title }}</h2>
        <p class="photoDesc">{{ description }}</p>

      </div>
    </div>
    <div class="close" @click="$emit('closeModal')" />
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },

  props: {
    item: {
      type: Object,
      required: true,
    },
  },

  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
  },
};
</script>

<style lang="scss" scoped>
  .outerWrapper {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    color: #000;
    background: #f6f6f6;
    z-index: 10;

    @media (min-width: 1024px) {
      max-width: 70%;
      height: 60%;
      min-height: 515px;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
    }
  }

  .description {
    color: #333;
    max-width: 100%;

    @media(min-width: 1024px) {
      max-width: 40%;
    }
  }

  .photoDesc {
    max-height: 285px;
    overflow-y: scroll;
    padding: 0 10px 0;
    margin: 0;
    word-wrap: break-word;

    &::-webkit-scrollbar {
    width: 4px;
    }

    &::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 6px rgb(236, 236, 236);
    }

    &::-webkit-scrollbar-thumb {
      background-color: rgb(34, 211, 235);
      outline: 1px solid slategrey;
    }
  }

  .innerWrapper {
    display: flex;
    height: 100%;
    padding: 40px 15px 10px 15px;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    .photo {
      max-width: 990px;
      height: auto;
      background: #000;

      >img {
        width: 100%;
        max-height: 140px;
        object-fit: cover;

        @media (min-width: 1024px) {
          max-height: 500px;
        }
      }
    }

    @media (min-width: 1024px) {
      flex-direction: row;
      .photo {
        min-width: 50%;
        margin-right: 20px;
      }
    }
  }

  .close {
      position: absolute;
      width: 30px;
      height: 30px;
      padding: 30px;
      right: 0;
      top: 0;
      cursor: pointer;
      &::before,
      &::after {
        position: absolute;
        top: 30px;
        right: 20px;
        content: '';
        width: 20px;
        height: 2px;
        background: black;
        display: block;
      }
      &::before {
        transform: rotate(45deg);
      }
      &::after {
        transform: rotate(-45deg);
      }
    }
</style>
