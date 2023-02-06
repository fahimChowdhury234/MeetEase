<template>
  <div id="app">
    <div class="">
      <navbar :currentUser="currentUser"/>
      <div class="bg-[#e8e8e8]">
        <router-view :currentUser="currentUser"/>
        <!-- <router-view v-slot="{ Component }">
          <component :is="Component" :currentUser="currentUser" />
        </router-view> -->
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase/compat/app";
import "firebase/compat/auth";
import { getAuth, signOut } from "firebase/auth";
import navbar from "./components/NavBar.vue";

export default {
  name: "App",
  components: {
    navbar,
  },
  data() {
    return {
      currentUser: null,
    };
  },
  mounted() {
    this.currentUser = firebase.auth().currentUser;
  },
  methods: {
    logOut() {
      const auth = getAuth();
      signOut(auth)
        .then(() => {
          // Sign-out successful.
          this.$router.replace("login");
        })
        .catch((error) => {
          // An error happened.
          console.log(error);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: "Noto Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
}
.router-link-exact-active {
  color: #15a493 !important;
}
</style>
