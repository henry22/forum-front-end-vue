<template>
  <div class="container py-5">
    <AdminRestaurantForm @after-submit="handleAfterSubmit" :initial-restaurant="restaurant" />
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
      }
    };
  },
  created() {
    const { id } = this.$route.params;
    this.fetchRestaurant(id);
  },
  methods: {
    handleAfterSubmit(formData) {
      // 透過 API 將表單資料送到伺服器
      for (let [name, value] of formData.entries()) {
        console.log(`${name}: ${value}`);
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