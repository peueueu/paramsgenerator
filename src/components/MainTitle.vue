<template>
  <h1 class="main_title">{{ title }}</h1>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "Vamo gerar?",
    },
  },
};
</script>

<style>
.main_title {
  color: #f2f2f2;
  font-weight: bold;
  font-size: 4rem;
  padding-bottom: 60px;
  font-family: "Lobster";
}
</style>
