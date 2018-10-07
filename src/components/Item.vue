<template>
  <div class="item" :style="style"></div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
};
</script>

<style lang="scss" scoped>
  .item {
    cursor: pointer;
    width: 100%;
    height: 250px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    position: relative;
    overflow: hidden;

    &::after {
      content: '';
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background: rgba(255,255,255,0.4);
      opacity: 0;
      transition: opacity 0.4s;
    }

    &:hover {
      transition: 0.4s;
      box-shadow: 0px 2px 10px 1px rgba(0,0,0,0.5);
    }

    &:hover::after {
      transition: opacity 0.4s;
      opacity: 1;
    }


    @media (min-width: 768px){
      width: 25vw;
    }
  }

</style>
