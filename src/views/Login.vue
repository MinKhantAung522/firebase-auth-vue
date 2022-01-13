<template>
  <div class="d-flex justify-content-center">
    <form @submit.prevent="login" class="text-start">
      <div class="form-group mb-3">
        <label for="exampleFormControlInput1">Email address:</label>
        <input
          type="email"
          class="form-control mt-2"
          placeholder="name@example.com"
          v-model="user.email"
        />
      </div>
      <div class="form-group mb-3">
        <label for="exampleFormControlInput1">Password:</label>
        <input
          type="password"
          class="form-control mt-2"
          placeholder="password"
          v-model="user.password"
        />
      </div>
      <button type="submit" class="my-3 btn btn-success">Login</button>
    </form>
  </div>
</template>

<script>
import { app as firebaseApp } from "../firebase/firebase";
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
export default {
  data() {
    return {
      user: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    login() {
      const auth = getAuth(firebaseApp);
      signInWithEmailAndPassword(auth, this.user.email, this.user.password)
        .then(() => {
          this.$router.push("/dashboard")
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
        });
    },
  },
};
</script>

<style>
</style>