<template>
  <div class="bg-login bg-login-1">
    <div class="row login-box">
      <img src="~/assets/images/logo-main1.png" />
      <h4></h4>
      <Loader v-if="loader" />
      <form method="post" @submit.prevent="login">
        <div class="mb-3">
          <label for="inputEmail">ID Pengguna</label>
          <input
            class="form-control"
            id="inputEmail"
            v-model="email"
            type="text"
          />
        </div>

        <div class="mb-3 password">
          <label for="inputPassword">Kata Laluan</label>
          <a class="small ml-auto forgot-password" href="/app/forget-password"
            >Terlupa Kata Laluan?</a
          >
          <input
            class="form-control"
            id="inputPassword"
            v-model="password"
            type="password"
          />
        </div>
        <Error :message="emailerror" v-if="emailerror" />
        <div class="form-check d-flex align-items-center">
          <div class="">
            <input
              class="form-check-input"
              id="inputRememberPassword"
              type="checkbox"
              value=""
            />
            <label class="form-check-label" for="inputRememberPassword"
              >Ingat saya</label
            >
          </div>
        </div>
        <div class="d-flex align-items-center">
          <input type="submit" class="btn login-btn" value="Log Masuk" />
          <!-- <a class="btn login-btn" href="">Login</a> -->
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import Error from "~/components/Error";
import Loader from "../components/loader.vue";
export default {
  components: { Loader },
  name: "staff-login",
  head: {
    script: [
      {
        src: "/app/js/bootstrap.bundle.min.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "/app/js/scripts.js",
        body: true,
        crossorigin: "anonymous",
      },
    ],
  },
  data() {
    return {
      loader: false,
      email: "",
      password: "",
      emailerror: null,
      passerror: null,
      userdetail: null,
    };
  },
  methods: {
    async login() {
      this.emailerror = null;
      this.passerror = null;
      try {
        if (!this.email) {
          this.emailerror = "Email is Required!";
        }
        if (!this.password) {
          this.passerror = "Password is Required!";
        }
        if (this.email && this.password) {
          this.loader = true;
          const response = await this.$axios.post("auth/login", {
            email: this.email,
            password: this.password,
            type:""
          });
          this.userdetail = response.data;
          const response2 = await this.$axios.get(
              "system-settings/get-setting/idle-session-timeout"
            );
          this.idleTimeout = parseInt(response2.data.setting[0].variable_value);

          if (this.userdetail.code == 200) {
            localStorage.setItem(
              "userdetails",
              JSON.stringify(this.userdetail)
            );
            localStorage.setItem(
              "idleTimeout",
              JSON.stringify(this.idleTimeout)
            );
            this.loader = false;
            this.$router.push(this.userdetail.route_alt);
          } else {
            this.loader = false;
            this.emailerror = this.userdetail.message;
          }
        }
      } catch (e) {
        console.log("my error", e);
        console.log("api not working");
        this.loader = false;
        this.emailerror = "ID Pengguna atau Kata Laluan Tidak Sah"; //$user.message.email; //e.response.data.message;
      }
      console.log("my data", this.userdetail);
    },
  },
};
</script>
