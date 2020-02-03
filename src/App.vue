<template>
  <div id="app">
    <navbar v-on:click="changeCurrentView" />
    <div class="imageCell" v-if="currentView === 'ALL_PHOTOS'">
      <!-- eslint-disable-next-line -->
      <allphotos
        v-for="photo in photos"
        :key="photo.key"
        :image="photo.base64"
        :selectOnePhoto="selectOnePhoto"
      />
    </div>
    <!-- eslint-disable-next-line  -->
    <singlephoto v-if="currentView === 'SINGLE_PHOTO'" :selectedPhoto="selectedPhoto" />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import SinglePhoto from "./components/SinglePhoto";
import { listObjects, getSingleObject } from "../utils/index";
import shortid from "shortid";

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allphotos: AllPhotos,
    singlephoto: SinglePhoto
  },
  data: () => ({
    title: "Photo Upload App",
    currentView: "ALL_PHOTOS",
    photos: [],
    selectedPhoto: ""
  }),
  created: function() {
    listObjects().then(data => {
      Promise.all(data.map(el => getSingleObject(el.Key))).then(
        data =>
          (this.photos = data.map(base64 => ({
            base64,
            key: shortid.generate()
          })))
      );
    });
  },
  methods: {
    changeCurrentView() {
      this.currentView = "ALL_PHOTOS";
    },
    selectOnePhoto(photoData) {
      this.currentView = "SINGLE_PHOTO";
      this.selectedPhoto = photoData;
    }
  }
};
</script>

<style scoped>
#app {
  text-align: center;
}
.imageCell {
  display: inline-block;
  margin: 10px;
  width: 100%;
}
</style>
