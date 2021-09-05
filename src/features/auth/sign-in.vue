<template>
  <form action="#" @submit.prevent="submit" class="sign-in-htm">
    <div class="group">
      <label
        :class="{ invalid: $v.username.$invalid && $v.username.$dirty }"
        for="sign-in-user"
        class="label"
        >Username</label
      >
      <input
        :class="{ invalid: $v.username.$invalid && $v.username.$dirty }"
        id="sign-in-user"
        type="text"
        class="input"
        @input="$v.username.$touch()"
        v-model="username"
      />
    </div>
    <div class="group">
      <label
        :class="{ invalid: $v.password.$invalid && $v.password.$dirty }"
        for="sign-in-pass"
        class="label"
        >Password</label
      >
      <input
        :class="{ invalid: $v.password.$invalid && $v.password.$dirty }"
        id="sign-in-pass"
        type="password"
        class="input"
        data-type="password"
        @input="$v.password.$touch()"
        v-model="password"
      />
    </div>
    <div class="group">
      <input id="check" type="checkbox" class="check" v-model="keepSignedIn" />
      <label for="check"><span class="icon"></span> Keep me Signed in</label>
    </div>
    <div class="group">
      <input type="submit" class="button" value="Sign In" />
    </div>
    <div class="hr"></div>
    <div class="foot-lnk">
      <a href="#forgot">Forgot Password?</a>
    </div>
  </form>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
  mounted() {
    this.$bus.$on("navigate", this.reset);
  },
  validations: {
    username: {
      required,
    },
    password: {
      required,
    },
  },
  data() {
    return {
      username: "",
      password: "",
      keepSignedIn: true,
    };
  },
  computed: {
    isValid() {
      return !this.$v.username.$invalid && !this.$v.password.$invalid;
    },
  },
  methods: {
    submit() {
      if (!this.$v.$invalid) {
        this.$emit("do-sign-in", { ...this.$data });
      } else {
          this.$v.$touch()
      }
    },
    reset(selected) {
      if (selected === "signup") {
        this.username = "";
        this.password = "";
        this.keepSignedIn = true;
        this.$v.$reset()
      }
    },
  },
};
</script>