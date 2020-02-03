<template>
  <div>
    <a href="#">
      <h1 v-on:click="$emit('click')">{{ title }}</h1>
    </a>
    <upload />
  </div>
</template>

<script>
import Upload from "./Upload";

export default {
  name: "Navbar",
  components: {
    upload: Upload
  },
  data: () => ({
    title: "Photo Upload App"
  }),
  props: ["click"]
};
</script>

<style></style>
