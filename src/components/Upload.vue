<template>
  <div>
    <input id="input" type="file" @change="uploadImage" />
    <button v-on:click="getElementById">Choose File</button>
  </div>
</template>

<script>
import { saveObject } from "../../utils/index";
export default {
  name: "Upload",
  methods: {
    getElementById() {
      document.getElementById("input").click();
    },
    uploadImage() {
      saveObject(document.getElementById("input").files[0]);
    }
  }
};
</script>

<style scoped>
input {
  position: absolute;
  left: 999999999px;
}
</style>
