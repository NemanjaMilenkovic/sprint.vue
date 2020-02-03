<template>
  <img
    :src="'data:image/png;base64, ' + image"
    v-on:click="selectOnePhoto('data:image/png;base64, ' + image)"
  />
</template>

<script>
export default {
  name: "AllPhotos",
  props: ["image", "selectOnePhoto"]
};
</script>

<style scoped>
img {
  cursor: pointer;
  max-width: 20%;
}
</style>
