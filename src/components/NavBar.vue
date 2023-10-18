<template>
  <div class="bg-[#f7f7f7] z-50 sticky top-0 border-b md:border-b-0 Navbar_navbar__h7fWf">
    <div class="w-full">
      <div class="container px-5 flex  items-center py-4  mx-auto justify-between relative lg:w-[1350px] ">
        <div class="lg:flex-1">
          <!-- <a class="btn btn-ghost normal-case text-xl">daisyUI</a> -->
          <router-link to="/">
            <img class="w-44 object-cover" src="../assets/img/logo.png" alt="" />
          </router-link>
        </div>
        <div class="flex-none gap-x-28 hidden items-center  lg:flex">
          <ul class="flex items-center gap-12">
            <router-link to="/"
              class="text-base rounded-md font-medium text-gray cursor-pointer transition-all hover:text-prim"
              :class="currentUser ? 'hidden' : ''" href="#">Home</router-link>
            <router-link to="/login"
              class="text-base rounded-md font-medium text-gray cursor-pointer transition-all hover:text-prim"
              :class="currentUser ? 'hidden' : ''" href="#">Log in</router-link>
          </ul>
          <div class="" v-if="!currentUser">
            <router-link to="/signup">
              <button
                class="signup flex items-center gap-1 justify-center w-36 py-2 text-base rounded-full font-medium border bg-prim text-white transition-all hover:bg-prim-dark active:bg-prim">
                <span>Sign up </span>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5">
                  <path fill-rule="evenodd"
                    d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z"
                    clip-rule="evenodd" />
                </svg>
              </button>
            </router-link>
          </div>
          <div class="" v-else>
            <button
              class="signup flex items-center gap-1 justify-center w-36 py-2 text-base rounded-full font-medium border bg-prim text-white transition-all hover:bg-prim-dark active:bg-prim"
              @click="logOut">
              <span>Log Out </span>
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5">
                <path fill-rule="evenodd"
                  d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z"
                  clip-rule="evenodd" />
              </svg>
            </button>
          </div>
        </div>
        <div class="block lg:hidden" @click="isOpen = !isOpen">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
            class="w-6 h-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
          </svg>

        </div>
        <div class="absolute top-16 right-6  bg-white border border-gray border-opacity-50 px-5 py-5 rounded-lg " v-if="isOpen">
          <ul class="flex items-start flex-col gap-6 pl-4">
            <router-link to="/"
              class="text-sm rounded-md font-medium text-gray cursor-pointer transition-all hover:text-prim"
              :class="currentUser ? 'hidden' : ''" href="#">Home</router-link>
            <router-link to="/login"
              class="text-sm rounded-md font-medium text-gray cursor-pointer transition-all hover:text-prim"
              :class="currentUser ? 'hidden' : ''" href="#">Log in</router-link>
          </ul>
          <div class="mt-4" v-if="!currentUser">
            <router-link to="/signup">
              <button
                class="signup flex items-center gap-1 justify-center w-32 text-sm  py-2  rounded-full font-medium border bg-prim text-white transition-all hover:bg-prim-dark active:bg-prim">
                <span>Sign up </span>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5">
                  <path fill-rule="evenodd"
                    d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z"
                    clip-rule="evenodd" />
                </svg>
              </button>
            </router-link>
          </div>
          <div class="mt-4" v-else>
            <button
              class="signup flex items-center gap-1 justify-center w-32 text-sm py-2 rounded-full font-medium border bg-prim text-white transition-all hover:bg-prim-dark active:bg-prim"
              @click="logOut">
              <span>Log Out </span>
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5">
                <path fill-rule="evenodd"
                  d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z"
                  clip-rule="evenodd" />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import firebase from "firebase/compat/app";
// import "firebase/compat/auth";
import { getAuth, signOut } from "firebase/auth";

export default {
  // props:['currentUser'],
  props: {
    currentUser: [String, Object],
  },
  data() {
    return {
      // currentUser: null,
      isOpen:false
    };
  },
  // mounted() {
  //   this.currentUser = firebase.auth().currentUser;
  // },
  methods: {
    logOut() {
      const auth = getAuth();
      signOut(auth)
        .then(() => {
          // Sign-out successful.
          this.$router.replace("login");
          this.$toast("sucessfully log out");
        })
        .catch((error) => {
          // An error happened.
          console.log(error);
        });
    },
  },
};
</script>

<style scoped></style>
