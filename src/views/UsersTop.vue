<template>
  <div class="container py-5">
    <!-- 使用 NavTabs 元件 -->
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <UserCard v-for="user in users" :key="user.id" :initial-user="user" />
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import UserCard from "./../components/UserCard";
import usersApi from "./../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  name: "usersTop",
  components: {
    NavTabs,
    UserCard
  },
  data() {
    return {
      users: []
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
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法取得美食達人，請稍後再試"
        });
      }
    }
  }
};
</script>