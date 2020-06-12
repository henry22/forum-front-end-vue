<template>
  <div class="container py-5">
    <!-- 使用 NavTabs 元件 -->
    <NavTabs />

    <Spinner v-if="isLoading" />
    <template v-else>
      <h1 class="mt-5">美食達人</h1>
      <hr />
      <div class="row text-center">
        <UserCard v-for="user in users" :key="user.id" :initial-user="user" />
      </div>
    </template>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import UserCard from "./../components/UserCard";
import Spinner from "./../components/Spinner";
import usersApi from "./../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  name: "usersTop",
  components: {
    NavTabs,
    UserCard,
    Spinner
  },
  data() {
    return {
      users: [],
      isLoading: true
    };
  },
  created() {
    this.fetchTopUsers();
  },
  methods: {
    async fetchTopUsers() {
      try {
        const { data } = await usersApi.getTopUsers();

        this.users = data.users.map(user => ({
          id: user.id,
          name: user.name,
          image: user.image,
          followerCount: user.FollowerCount,
          isFollowed: user.isFollowed
        }));

        this.isLoading = false;
      } catch (error) {
        console.log("error", error);
        this.isLoading = false;

        Toast.fire({
          icon: "error",
          title: "無法取得美食達人，請稍後再試"
        });
      }
    }
  }
};
</script>