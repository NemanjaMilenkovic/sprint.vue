<script>
// import { currentView, selectedPhoto } from "./App";
import Vuex from "vuex";
import Vue from "vue";
Vue.use(Vuex);

import { listObjects, getSingleObject } from "../utils/index";
import shortid from "shortid";

export default new Vuex.Store({
  state: {
    title: "Photo Upload App",
    currentView: "ALL_PHOTOS",
    photos: [],
    selectedPhoto: "",
    photosLoaded: false
  },
  mutations: {
    setAllPhotos: state => {
      listObjects().then(data => {
        Promise.all(data.map(el => getSingleObject(el.Key)))
          .then(
            data =>
              (state.photos = data.map(base64 => ({
                base64,
                key: shortid.generate()
              })))
          )
          .then(() => (state.photosLoaded = true));
      });
    },
    changeCurrentView: state => (state.currentView = "ALL_PHOTOS"),
    selectOnePhoto: (state, photoData) => {
      state.currentView = "SINGLE_PHOTO";
      state.selectedPhoto = photoData;
    }
  }
});
</script>
