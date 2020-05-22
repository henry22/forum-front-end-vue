// ./src/views/SignIn.vue
<template>
  <div class="container py-5">
    <form class="w-100" @submit.prevent.stop="handleSubmit">
      <div class="text-content mb-4">
        <h1 class="h3 mb-3 font-weight-normal">Sign In</h1>
      </div>

      <div class="form-label-group mb-2">
        <label for="email">email</label>
        <input
          type="email"
          id="email"
          name="email"
          class="form-control"
          placeholder="email"
          autocomplete="username"
          required
          autofocus
          v-model="email"
        />
      </div>

      <div class="form-label-group mb-3">
        <label for="password">password</label>
        <input
          type="password"
          id="password"
          name="password"
          class="form-control"
          placeholder="Password"
          autocomplete="current-password"
          required
          v-model="password"
        />
      </div>

      <button class="btn btn-lg btn-primary btn-block mb-3" type="submit">Submit</button>

      <div class="text-center mb-3">
        <p>
          <router-link to="/signup">Sign Up</router-link>
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
      email: '',
      password: ''
    }
  },
  methods: {
    handleSubmit() {
      const data = JSON.stringify({
        email: this.email,
        password: this.password
      })

      // TODO: 向後端驗證使用者登入資訊是否合法
      console.log('data', data)
    }
  }
}
</script>