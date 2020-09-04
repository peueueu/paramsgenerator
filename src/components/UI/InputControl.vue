<template>
  <div class="input-wrapper">
    <label :for="name">{{ name }}</label>
    <input type="text" v-on="$listeners" />
  </div>
</template>

<script>
export default {
  name: "InputControl",
  props: {
    name: {
      type: String,
      required: true,
    },
    url: {
      type: String,
    },
  },
};
</script>

<style lang="scss" scoped>
.input-wrapper {
  display: flex;
  flex-direction: column;

  label {
    font-size: 1.25rem;
    font-weight: bold;
    margin-bottom: 8px;
    text-transform: uppercase;
    color: white;
  }

  input {
    padding: 5px;
    font-size: 1rem;
    color: #1a1a1a;
    font-weight: bold;
    margin-bottom: 10px;
    border-radius: 5px;
    border-left: 6px solid #44d3ce;

    &:focus {
      box-shadow: 0px 3px 6px #44d3ce;
      filter: blur(0.2);
    }
  }
}
</style>
