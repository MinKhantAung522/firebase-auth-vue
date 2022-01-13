<template>
  <div class="d-flex justify-content-center">
    <form @submit.prevent="signup" class="text-start">
      <div class="form-group mb-3">
        <label for="exampleFormControlInput1">Name:</label>
        <input
          type="text"
          class="form-control mt-2"
          placeholder="first name"
          v-model="user.name"
        />
      </div>
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
      <button type="submit" class="my-3 btn btn-success">SignUp</button>
    </form>
  </div>
</template>

<script>
import { app as firebaseApp } from "../firebase/firebase";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
export default {
  data() {
    return {
      user: {
        name: "",
        email: "",
        password: "",
      },
    };
  },
  methods: {
    signup() {
      const auth = getAuth(firebaseApp);
      createUserWithEmailAndPassword(auth, this.user.email, this.user.password)
        .then(() => {
          this.$router.push("/login")
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
          // ..
        });
    },
  },
};
</script>

<style>
</style>