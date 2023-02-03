<template>
  <div>
    <h1>{{ uName }}</h1>
  </div>
</template>

<script>
import firebase from "firebase/compat/app";
import "firebase/compat/auth";

export default {
  data() {
    return {
      uName: null,
    };
  },
  async mounted() {
    await firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        // User is signed in.
        console.log();
        this.uName = user.displayName;
      } else {
        // No user is signed in.
      }
    });
  },
};
</script>

<style></style>
