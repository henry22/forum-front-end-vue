<template>
  <div>
    <h2 class="my-4">所有評論：</h2>
    <div v-for="restaurantComment in restaurantComments" :key="restaurantComment.id">
      <blockquote class="blockquote mb-0">
        <button
          type="button"
          class="btn btn-danger float-right"
          v-if="currentUer.isAdmin"
          @click.stop.prevent="handleDeleteButtonClick(restaurantComment.id)"
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

const dummyUser = {
  currentUser: {
    id: 1,
    name: "管理者",
    email: "root@example.com",
    image: "https://i.pravatar.cc/300",
    isAdmin: true
  },
  isAuthenticated: true
};

export default {
  // 透過 mixins 屬性將撰寫好的 mixin 放入
  mixins: [fromNowFilter],
  props: {
    restaurantComments: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      currentUer: dummyUser.currentUser
    };
  },
  methods: {
    handleDeleteButtonClick(commentId) {
      console.log("handleDeleteButtonClick", commentId);
      // TODO: 請求 API 伺服器刪除 id 為 commentId 的評論
      // 觸發父層事件 - $emit( '事件名稱' , 傳遞的資料 )
      this.$emit("after-delete-comment", commentId);
    }
  }
};
</script>