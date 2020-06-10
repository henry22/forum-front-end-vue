<template>
  <div class="container py-5">
    <AdminRestaurantForm
      @after-submit="handleAfterSubmit"
      :initial-restaurant="restaurant"
      :is-processing="isProcessing"
    />
  </div>
</template>

<script>
import AdminRestaurantForm from "./../components/AdminRestaurantForm";
// STEP 1: 載入 adminAPI 和 Toast
import adminApi from "./../apis/admin";
import { Toast } from "./../utils/helpers";

export default {
  name: "AdminRestaurantEdit",
  components: {
    AdminRestaurantForm
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryId: "",
        tel: "",
        address: "",
        description: "",
        image: "",
        openingHours: ""
      },
      isProcessing: false
    };
  },
  created() {
    const { id } = this.$route.params;
    this.fetchRestaurant(id);
  },
  beforeRouteUpdate(to, from, next) {
    // 路由改變時重新抓取資料
    const { id } = to.params;
    this.fetchRestaurant(id);
    next();
  },
  methods: {
    async handleAfterSubmit(formData) {
      try {
        this.isProcessing = true;

        const { data } = await adminApi.restaurants.update({
          restaurantId: this.restaurant.id,
          formData
        });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.$router.push({ name: "admin-restaurants" });
      } catch (error) {
        console.log("error", error);
        this.isProcessing = false;

        Toast.fire({
          icon: "error",
          title: "無法更新餐廳資料，請稍後再試"
        });
      }
    },
    // STEP 2: 改成 async...await 語法
    async fetchRestaurant(restaurantId) {
      try {
        const { data } = await adminApi.restaurants.getDetail({ restaurantId });

        // STEP 3: 透過解構賦值將需要的資料取出
        const {
          id,
          name,
          CategoryId: categoryId,
          tel,
          address,
          description,
          image,
          opening_hours: openingHours
        } = data.restaurant;

        // STEP 4: 將資料帶入 Vue 內
        this.restaurant = {
          ...this.restaurant,
          id,
          name,
          categoryId,
          tel,
          address,
          description,
          image,
          openingHours
        };
      } catch (error) {
        console.log("error", error);
        //  STEP 5: 錯誤處理
        Toast.fire({
          icon: "error",
          title: "無法取得餐廳資料，請稍後再試"
        });
      }
    }
  }
};
</script>