<template>
  <div class="content-output-wrapper">
    <div class="wrapper">
      <div class="content-response" v-on="$listeners">{{ content }}</div>
      <input type="hidden" :value="content" :id="id" />
    </div>
    <span class="tip">Click in the the box to copy to clipboard. :)</span>
  </div>
</template>

<script>
export default {
  props: {
    content: {
      type: String,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
.wrapper {
  padding: 10px;
  border: 2px solid #35a592;
  border-radius: 5px;
  overflow-y: scroll;
  height: 150px;
}
.content-response {
  max-width: 500px;
  cursor: pointer;
}
.tip {
  display: block;
  margin-top: 10px;
  color: #2a2a2a;
  font-size: 0.85rem;
  font-weight: 400;
}
</style>
