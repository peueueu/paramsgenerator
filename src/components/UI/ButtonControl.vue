<template>
  <button class="btnGen" v-on="$listeners">{{ name }}</button>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: false,
    },
  },
};
</script>

<style lang="scss">
.btnGen {
  max-width: 200px;
  margin: 20px auto 0;
  padding: 5px 15px;
  border-radius: 8px;
  color: #fff;
  font-size: 1.25rem;
  border: none;
  font-weight: bold;
  background: #35a592;
}
</style>
