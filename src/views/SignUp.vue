<template>
  <div class="container py-5">
    <form class="w-100" @submit.prevent.stop="handleSubmit">
      <div class="text-center mb-4">
        <h1 class="h3 mb-3 font-weight-normal">Sign Up</h1>
      </div>

      <div class="form-label-group mb-2">
        <label for="name">Name</label>
        <input
          type="text"
          id="name"
          name="name"
          class="form-control"
          placeholder="name"
          autocomplete="username"
          required
          autofocus
          v-model="name"
        />
      </div>

      <div class="form-label-group mb-2">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          name="email"
          class="form-control"
          placeholder="email"
          autocomplete="email"
          required
          v-model="email"
        />
      </div>

      <div class="form-label-group mb-3">
        <label for="password">Password</label>
        <input
          type="password"
          id="password"
          name="password"
          class="form-control"
          placeholder="Password"
          autocomplete="new-password"
          required
          v-model="password"
        />
      </div>

      <div class="form-label-group mb-3">
        <label for="password-check">Password Check</label>
        <input
          type="password"
          id="password-check"
          name="passwordCheck"
          class="form-control"
          placeholder="Password"
          autocomplete="new-password"
          required
          v-model="passwordCheck"
        />
      </div>

      <button class="btn btn-lg btn-primary btn-block mb-3" type="submit">Submit</button>

      <div class="text-center mb-3">
        <p>
          <router-link to="/signin">Sign In</router-link>
        </p>
      </div>

      <p class="mt-5 mb-3 text-muted text-center">&copy; 2019-2020</p>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      password: "",
      passwordCheck: ""
    };
  },
  methods: {
    handleSubmit() {
      const data = JSON.stringify({
        name: this.name,
        email: this.email,
        password: this.password,
        passwordCheck: this.passwordCheck
      });

      // TODO: 向後端驗證使用者登入資訊是否合法
      console.log("data", data);
    }
  }
};
</script>