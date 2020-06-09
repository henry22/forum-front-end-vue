<template>
  <div class="col-3">
    <a href="#">
      <img :src="user.image | emptyImage" width="140px" height="140px" />
    </a>
    <h2>{{user.name}}</h2>
    <span class="badge badge-secondary">追蹤人數：{{user.followerCount}}</span>
    <p class="mt-3">
      <button
        type="button"
        class="btn btn-danger"
        v-if="user.isFollowed"
        @click.stop.prevent="deleteFollowing(user.id)"
      >取消追蹤</button>
      <button
        type="button"
        class="btn btn-primary"
        v-else
        @click.stop.prevent="addFollowing(user.id)"
      >追蹤</button>
    </p>
  </div>
</template>

<script>
import { emptyImageFilter } from "./../utils/mixins";
import usersApi from "./../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  name: "UserCard",
  mixins: [emptyImageFilter],
  props: {
    initialUser: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      user: this.initialUser
    };
  },
  methods: {
    async addFollowing(userId) {
      try {
        const { data } = await usersApi.addFollowing({ userId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.user = {
          ...this.user,
          followerCount: this.user.followerCount + 1,
          isFollowed: true
        };
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法加入追蹤，請稍後再試"
        });
      }
    },
    async deleteFollowing(userId) {
      try {
        const { data } = await usersApi.deleteFollowing({ userId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.user = {
          ...this.user,
          followerCount: this.user.followerCount - 1,
          isFollowed: false
        };
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法取消追蹤，請稍後再試"
        });
      }
    }
  }
};
</script>