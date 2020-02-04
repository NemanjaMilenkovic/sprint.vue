<template>
  <div id="app">
    <navbar v-on:click="changeCurrentView()" />
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

import store from "./Vuex";

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allphotos: AllPhotos,
    singlephoto: SinglePhoto
  },
  created: function() {
    store.commit("setAllPhotos");
  },
  computed: {
    title() {
      return store.state.title;
    },
    currentView() {
      return store.state.currentView;
    },
    photos() {
      return store.state.photos;
    },
    selectedPhoto() {
      return store.state.selectedPhoto;
    }
  },
  methods: {
    changeCurrentView() {
      store.commit("changeCurrentView");
      // store.state.currentView = "ALL_PHOTOS";
    },
    selectOnePhoto(photoData) {
      store.commit("selectOnePhoto", photoData);
      // store.state.currentView = "SINGLE_PHOTO";
      // store.state.selectedPhoto = photoData;
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
