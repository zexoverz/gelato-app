<template>
  <div>
    <!-- <section class="blog-banner-area" id="category">
      <div class="container h-100">
        <div class="blog-banner">
          <div class="text-center">
            <h1>Login Page</h1>
            <nav aria-label="breadcrumb" class="banner-breadcrumb">
              <ol class="breadcrumb">
                <li class="breadcrumb-item">
                  <a href="/">Home</a>
                </li>
                <li class="breadcrumb-item active" aria-current="page">Login</li>
              </ol>
            </nav>
          </div>
        </div>
      </div>
    </section>-->
    <!-- ================ end banner area ================= -->

    <!--================Login Box Area =================-->
    <section class="login_box_area section-margin">
      <div class="container">
        <div class="row">
          <div class="col-lg-6">
            <div class="login_box_img">
              <div class="hover">
                <h4>New to our website?</h4>
                <p>
                  There are advances being made in science and technology
                  everyday, and a good example of this is the
                </p>
                <!-- <a class="button button-account" href="/register">Create an Account</!-->
                <router-link to="/register" class="button button-account">Create an Account</router-link>
              </div>
            </div>
          </div>
          <div class="col-lg-6">
            <div class="login_form_inner">
              <h3>Log in to enter</h3>
              <form class="row login_form" action="#/" id="contactForm">
                <div class="col-md-12 form-group">
                  <input
                    type="text"
                    class="form-control"
                    id="name"
                    name="name"
                    placeholder="Email"
                    v-model="email"
                    onfocus="this.placeholder = ''"
                    onblur="this.placeholder = 'Email'"
                  />
                </div>
                <div class="col-md-12 form-group">
                  <input
                    type="password"
                    class="form-control password"
                    id="name"
                    name="name"
                    placeholder="Password"
                    v-model="password"
                    onfocus="this.placeholder = ''"
                    onblur="this.placeholder = 'Password'"
                  />
                </div>
                <div class="col-md-12 form-group">
                  <div class="creat_account">
                    <input type="checkbox" id="f-option2" name="selector" />
                    <label for="f-option2">Keep me logged in</label>
                  </div>
                </div>
                <div class="col-md-12 form-group">
                  <button type="button" v-on:click="login" class="button button-login w-100">Log In</button>
                  <!-- <a href="#">Forgot Password?</a> -->
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Swal from "sweetalert2";

export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    login() {
      let obj = {
        email: this.email,
        password: this.password
      };
      this.$store
        .dispatch("login", obj)

        .then(response => {
          localStorage.setItem("token", response.data.token);
          localStorage.setItem("username", response.data.name);
          Swal.fire("Good job!", "Login Success", "success");
          this.$store.commit("SET_LOGIN");
          if (localStorage.getItem("username") !== "admin") {
            this.$store.dispatch("getTransactions");
            this.$router.push("/");
          } else {
            this.$router.push("/");
          }
        })
        .catch(err => {
          if (err) {
            Swal.fire({
              icon: "error",
              title: "Oops...",
              text: "Invalid Email/Password!"
            });
          }
        });
    }
  }
};
</script>

<style></style>





  