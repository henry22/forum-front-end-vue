<template>
  <form @submit.stop.prevent="handleSubmit" v-show="!isLoading">
    <div class="form-group">
      <label for="name">Name</label>
      <input
        type="text"
        id="name"
        class="form-control"
        name="name"
        placeholder="Enter name"
        required
        v-model="restaurant.name"
      />
    </div>
    <div class="form-group">
      <label for="categoryId">Category</label>
      <select
        name="categoryId"
        id="categoryId"
        class="form-control"
        required
        v-model="restaurant.categoryId"
      >
        <option value selected disabled>--請選擇--</option>
        <option
          v-for="category in categories"
          :key="category.id"
          :value="category.id"
        >{{category.name}}</option>
      </select>
    </div>
    <div class="form-group">
      <label for="tel">Tel</label>
      <input
        type="text"
        id="tel"
        class="form-control"
        name="tel"
        placeholder="Enter telephone number"
        v-model="restaurant.tel"
      />
    </div>
    <div class="form-group">
      <label for="address">Address</label>
      <input
        type="text"
        id="address"
        class="form-control"
        name="address"
        placeholder="Enter address"
        v-model="restaurant.address"
      />
    </div>
    <div class="form-group">
      <label for="opening-hours">Opening Hours</label>
      <input
        type="time"
        id="opening-hours"
        class="form-control"
        name="opening_hours"
        v-model="restaurant.openingHours"
      />
    </div>
    <div class="form-group">
      <label for="description">Description</label>
      <textarea
        name="description"
        id="description"
        rows="3"
        class="form-control"
        v-model="restaurant.description"
      ></textarea>
    </div>
    <div class="form-group">
      <label for="image">Image</label>
      <img
        v-if="restaurant.image"
        :src="restaurant.image"
        class="d-block img-thumbnail mb-3"
        width="200"
        height="200"
      />
      <input
        type="file"
        id="image"
        name="image"
        accept="image/*"
        class="form-control-file"
        @change="handleFileChange"
      />
    </div>
    <button type="submit" class="btn btn-primary">送出</button>
  </form>
</template>

<script>
// STEP 1: 匯入 adminAPI 和錯誤提示用的 Toast
import adminApi from "./../apis/admin";
import { Toast } from "./../utils/helpers";

export default {
  name: "AdminRestaurantForm",
  props: {
    initialRestaurant: {
      type: Object,
      default: () => ({
        name: "",
        categoryId: "",
        tel: "",
        address: "",
        description: "",
        image: "",
        openingHours: ""
      })
    }
  },
  data() {
    return {
      restaurant: {
        name: "",
        categoryId: "",
        tel: "",
        address: "",
        description: "",
        image: "",
        openingHours: ""
      },
      categories: [],
      isLoading: true
    };
  },
  created() {
    this.fetchCategories();
    this.restaurant = {
      ...this.restaurant,
      ...this.initialRestaurant
    };
  },
  methods: {
    // STEP 2: 改成 async...await 語法
    async fetchCategories() {
      try {
        // STEP 3: 向伺服器取得餐廳類別清單
        const { data } = await adminApi.categories.get();

        this.categories = data.categories;
        this.isLoading = false;
      } catch (error) {
        console.log("error", error);
        this.isLoading = false;
        // STEP 4: 在 catch 中進行錯誤處理
        Toast.fire({
          icon: "error",
          title: "無法取得餐廳類別，請稍後再試"
        });
      }
      // this.categories = dummyData.categories;
    },
    handleFileChange(e) {
      const { files } = e.target;

      if (files.length === 0) {
        // 使用者沒有選擇上傳的檔案
        this.restaurant.image = "";
      } else {
        // 否則產生預覽圖
        const imageURL = window.URL.createObjectURL(files[0]);
        this.restaurant.image = imageURL;
      }
    },
    handleSubmit(e) {
      const form = e.target;
      const formData = new FormData(form);

      this.$emit("after-submit", formData);
    }
  }
};
</script>