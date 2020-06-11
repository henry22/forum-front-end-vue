<template>
  <nav class="navbar navbar-expand-lg fixed-top navbar-dark bg-dark">
    <router-link class="navbar-brand" to="/">餐廳評論網</router-link>

    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div id="navbarSupportedContent" class="navbar-collapse collapse">
      <div class="ml-auto d-flex align-items-center">
        <!-- is user is admin -->
        <router-link
          class="text-white mr-3"
          to="/admin/restaurants"
          v-if="currentUser.isAdmin"
        >管理員後台</router-link>
        <!-- is user is login -->
        <template v-if="isAuthenticated">
          <router-link
            class="text-white mr-3"
            :to="{name: 'user', params: {id: currentUser.id}}"
          >{{currentUser.name || '使用者'}} 您好</router-link>

          <button
            class="btn btn-small btn-outline-success my-2 my-sm-0"
            type="button"
            @click="logout"
          >登出</button>
        </template>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "Navbar",
  // 新增 `mapState` 方法
  computed: {
    ...mapState(["currentUser", "isAuthenticated"])
  },
  methods: {
    logout() {
      this.$store.commit("revokeAuthentication");
      this.$router.push('/signin')
    }
  }
};
</script>