<template>
  <div class="container py-5">
    <form @submit.stop.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          type="text"
          id="name"
          name="name"
          class="form-control"
          placeholder="Enter Name"
          required
          v-model="user.name"
        />
      </div>
      <div class="form-group">
        <label for="image">Image</label>
        <img
          v-if="user.image"
          :src="user.image"
          class="d-block img-thumbnail mb-3"
          width="200"
          height="200"
        />
        <input
          type="file"
          id="image"
          name="image"
          class="form-control-file"
          accept="image/*"
          @change="handleFileChange"
        />
      </div>
      <button
        type="submit"
        class="btn btn-primary"
        :disabled="isProcessing"
      >{{isProcessing ? '資料更新中...' : 'submit'}}</button>
    </form>
  </div>
</template>

<script>
import { mapState } from "vuex";
import usersApi from "./../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  name: "UserEdit",
  data() {
    return {
      user: {
        id: -1,
        name: "",
        image: "",
        email: ""
      },
      isProcessing: false
    };
  },
  created() {
    if (this.currentUser.id === -1) return;
    const { id } = this.$route.params;
    this.setUser(id);
  },
  computed: {
    ...mapState(["currentUser"])
  },
  watch: {
    currentUser(user) {
      if (user.id === -1) return;
      const { id } = this.$route.params;
      this.setUser(id);
    }
  },
  beforeRouteUpdate(to, from, next) {
    if (this.currentUser.id === -1) return;
    const { id } = to.params;
    this.setUser(id);
    next();
  },
  methods: {
    setUser(userId) {
      const { id, image, name, email } = this.currentUser;

      if (id.toString() !== userId.toString()) {
        this.$router.push({ name: "not-found" });
        return;
      }

      this.user = {
        ...this.user,
        id,
        image,
        name,
        email
      };
    },
    handleFileChange(e) {
      const { files } = e.target;

      if (files.length === 0) {
        // 使用者沒有選擇上傳的檔案
        this.user.image = "";
      } else {
        const imageURL = window.URL.createObjectURL(files[0]);
        this.user.image = imageURL;
      }
    },
    async handleSubmit(e) {
      try {
        if (!this.name) {
          Toast.fire({
            icon: "warning",
            title: "您尚未填寫姓名"
          });
          return;
        }

        const form = e.target;
        const formData = new FormData(form);

        this.isProcessing = true;

        const { data } = await usersApi.update({
          userId: this.id,
          formData
        });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.$router.push({ name: "user", params: { id: this.id } });
      } catch (error) {
        console.error(error.message);
        this.isProcessing = false;

        Toast.fire({
          icon: "error",
          title: "無法更新使用者資料，請稍後再試"
        });
      }
    }
  }
};
</script>