<template>
  <div>
    <div class="login-wrap">
      <div class="login-html">
        <input
          id="tab-1"
          type="radio"
          value="signin"
          v-model="navigation"
          @change="navigate"
          name="tab"
          class="sign-in"
          checked
        />
        <label for="tab-1" class="tab">Sign In</label>

        <input
          id="tab-2"
          type="radio"
          value="signup"
          v-model="navigation"
          @change="navigate"
          name="tab"
          class="sign-up"
        />
        <label for="tab-2" class="tab">Sign Up</label>

        <div class="login-form">
          <sign-in @do-sign-in="doSignIn" />
          <sign-up />
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import SignIn from "./sign-in.vue";
import SignUp from "./sign-up.vue";

export default {
  components: {
    SignIn,
    SignUp,
  },
  data() {
    return {
      navigation: "signup",
    };
  },
  methods: {
    navigate() {
      this.$bus.$emit('navigate', this.navigation)
    },
    doSignIn(obj) {
      //API
      window.console.log(obj)
    },
  },
};
</script>

<style src="./styles.css">
</style>
