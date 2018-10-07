<template>
  <input
  id="search"
  type="text"
  :class="{ dark }"
  name="search"
  :value="value"
  @input="handleChange">
</template>

<script>
export default {
  name: 'SearchInput',

  props: {
    value: {
      type: String,
      required: true,
    },

    dark: {
      type: Boolean,
      default: false,
    },
  },

  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },

};
</script>

<style lang="scss" scoped>
  input {
    width: 250px;
    margin: 40px 0 0 0;
    height: 30px;
    border: 0;
    border-bottom: 1px solid #fff;
    color: #fff;
    background: transparent;
    transition: box-shadow 0.5s;
    text-align: center;
    font-size: 1.2rem;

    &:focus {
      outline: none;
      border-bottom: 1px solid rgb(252, 215, 49);
      box-shadow: 0 15px 15px -8px rgba(252, 215, 49, 0.15);
    }

    @media(min-width: 768px) {
  font-size: 1.4rem;
}
}
.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;
  margin-top: 70px;
}

  label {
    font-family: 'Montserrat', sans-serif;
}

@media(min-width: 768px) {
  width: 350px;
}
</style>
