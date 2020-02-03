<template>
  <img :src="selectedPhoto" />
</template>

<script>
export default {
  name: "SinglePhoto",
  props: ["selectedPhoto"]
};
</script>

<style>
img {
  max-width: 100%;
}
</style>
