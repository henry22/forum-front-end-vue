<template>
  <div class="container py-5">
    <!-- 1. 使用先前寫好的 AdminNav -->
    <AdminNav />

    <form class="my-4">
      <div class="form-row">
        <div class="col-auto">
          <input type="text" class="form-control" placeholder="新增餐廳類別..." v-model="newCategoryName" />
        </div>
        <div class="col-auto">
          <button
            type="button"
            class="btn btn-primary"
            @click.stop.prevent="createCategory"
            :disabled="isProcessing"
          >新增</button>
        </div>
      </div>
    </form>

    <Spinner v-if="isLoading" />
    <table class="table" v-else>
      <thead class="thead-dark">
        <tr>
          <th scope="col" width="60">#</th>
          <th scope="col">Category Name</th>
          <th scope="col" width="210">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="category in categories" :key="category.id">
          <th scope="row">{{category.id}}</th>
          <td class="position-relative">
            <div class="category-name" v-show="!category.isEditing">{{category.name}}</div>
            <input
              type="text"
              class="form-control"
              v-model="category.name"
              v-show="category.isEditing"
            />
            <span
              class="cancel"
              v-show="category.isEditing"
              @click.stop.prevent="handleCancel(category.id)"
            >✕</span>
          </td>
          <td class="d-flex justify-content-between">
            <button
              type="button"
              class="btn btn-link mr-2"
              v-show="!category.isEditing"
              @click.stop.prevent="toggleIsEditing(category.id)"
            >Edit</button>
            <button
              type="button"
              class="btn btn-link mr-2"
              v-show="category.isEditing"
              @click.stop.prevent="updateCategory({categoryId: category.id, name: category.name})"
            >Save</button>
            <button
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="deleteCategory(category.id)"
            >Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from "./../components/AdminNav";
import Spinner from "./../components/Spinner";
import adminApi from "./../apis/admin";
import { Toast } from "./../utils/helpers";

export default {
  name: "AdminCategories",
  components: {
    AdminNav,
    Spinner
  },
  // 3. 定義 Vue 中使用的 data 資料
  data() {
    return {
      categories: [],
      newCategoryName: "",
      isProcessing: false,
      isLoading: true
    };
  },
  // 5. 調用 `fetchCategories` 方法
  created() {
    this.fetchCategories();
  },
  methods: {
    // 4. 定義 `fetchCategories` 方法，把 `dummyData` 帶入 Vue 物件
    async fetchCategories() {
      try {
        const { data } = await adminApi.categories.get();

        // 在每一個 category 中都添加一個 isEditing 屬性
        this.categories = data.categories.map(category => ({
          ...category,
          isEditing: false,
          nameCached: ""
        }));

        this.isLoading = false;
      } catch (error) {
        console.log("error", error);
        this.isLoading = false;

        Toast.fire({
          icon: "error",
          title: "無法取得餐廳類別，請稍後再試"
        });
      }
    },
    async createCategory() {
      try {
        this.isProcessing = true;

        const { data } = await adminApi.categories.create({
          name: this.newCategoryName
        });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        // 將新的類別添加到陣列中
        this.categories.push({
          id: data.categoryId,
          name: this.newCategoryName,
          isEditing: false
        });

        // 清空原本欄位中的內容
        this.newCategoryName = "";
      } catch (error) {
        console.log("error", error);
        this.isProcessing = false;

        Toast.fire({
          icon: "error",
          title: "無法新增餐廳類別，請稍後再試"
        });
      }
    },
    async deleteCategory(categoryId) {
      try {
        const { data } = await adminApi.categories.delete({ categoryId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        Toast.fire({
          icon: "success",
          title: "成功刪除該餐廳類別"
        });

        // 將該餐廳類別從陣列中移除
        this.categories = this.categories.filter(
          category => category.id !== categoryId
        );
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法刪除該餐廳類別，請稍後再試"
        });
      }
    },
    toggleIsEditing(categoryId) {
      this.categories = this.categories.map(category => {
        if (category.id === categoryId) {
          return {
            ...category,
            isEditing: !category.isEditing,
            nameCached: category.name
          };
        }

        return category;
      });
    },
    async updateCategory({ categoryId, name }) {
      try {
        const { data } = await adminApi.categories.update({ categoryId, name });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.toggleIsEditing(categoryId);
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法更新餐廳類別，請稍後再試"
        });
      }
    },
    handleCancel(categoryId) {
      this.categories = this.categories.map(category => {
        if (category.id === categoryId) {
          return {
            ...category,
            // 把原本的餐廳類別名稱還回去
            name: category.nameCached
          };
        }

        return category;
      });

      this.toggleIsEditing(categoryId);
    }
  }
};
</script>

<style scoped>
.category-name {
  padding: 0.375rem 0.75rem;
  border: 1px solid transparent;
  outline: 0;
  cursor: auto;
}

.btn-link {
  width: 62px;
}

.cancel {
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 25px;
  height: 25px;
  border: 1px solid #aaaaaa;
  border-radius: 50%;
  user-select: none;
  cursor: pointer;
  font-size: 12px;
}
</style>