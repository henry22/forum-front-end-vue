<template>
  <div>
    <h2 class="my-4">所有評論：</h2>
    <div v-for="restaurantComment in restaurantComments" :key="restaurantComment.id">
      <blockquote class="blockquote mb-0">
        <button
          type="button"
          class="btn btn-danger float-right"
          v-if="currentUser.isAdmin"
          @click.stop.prevent="handleDeleteButtonClick(restaurantComment.id)"
          :disabled="isProcessing"
        >Delete</button>
        <h3>
          <router-link
            :to="{name: 'user', params: {id: restaurantComment.User.id}}"
          >{{restaurantComment.User.name}}</router-link>
        </h3>
        <p>{{restaurantComment.text}}</p>
        <footer class="blockquote-footer">{{restaurantComment.createdAt | fromNow}}</footer>
      </blockquote>
      <hr />
    </div>
  </div>
</template>

<script>
// 載入撰寫好的 mixin
import { fromNowFilter } from "./../utils/mixins";
import commentsApi from "./../apis/comments";
import { Toast } from "./../utils/helpers";
import { mapState } from "vuex";

export default {
  // 透過 mixins 屬性將撰寫好的 mixin 放入
  mixins: [fromNowFilter],
  props: {
    restaurantComments: {
      type: Array,
      required: true
    }
  },
  computed: {
    ...mapState(["currentUser"])
  },
  data() {
    return {
      isProcessing: false
    };
  },
  methods: {
    async handleDeleteButtonClick(commentId) {
      try {
        this.isProcessing = true;
        const { data } = await commentsApi.delete({ commentId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        // 觸發父層事件 - $emit( '事件名稱' , 傳遞的資料 )
        this.$emit("after-delete-comment", commentId);

        Toast.fire({
          icon: "success",
          title: "移除評論成功"
        });
        this.isProcessing = false;
      } catch (error) {
        console.error(error.message);
        this.isProcessing = false;

        Toast.fire({
          icon: "error",
          title: "無法移除評論，請稍後再試"
        });
      }
    }
  }
};
</script>

<style scoped>
  h2.my-4 {
    margin-bottom: 1rem !important;
    font-size: 18px;
  }

  h3 {
    margin-bottom: 3px;
    line-height: 1.3;
  }

  .blockquote-footer {
    font-size: 12.5px;
  }
</style>>