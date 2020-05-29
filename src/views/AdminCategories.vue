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
          <button type="button" class="btn btn-primary" @click.stop.prevent="createCategory">新增</button>
        </div>
      </div>
    </form>

    <table class="table">
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
import { v4 as uuidv4 } from "uuid";

//  2. 定義暫時使用的資料
const dummyData = {
  categories: [
    {
      id: 1,
      name: "中式料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-17T03:45:22.000Z"
    },
    {
      id: 2,
      name: "日本料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
    {
      id: 3,
      name: "義大利料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
    {
      id: 4,
      name: "墨西哥料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
    {
      id: 5,
      name: "素食料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
    {
      id: 6,
      name: "美式料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-04-07T09:46:10.000Z"
    },
    {
      id: 1592,
      name: "dark cousine",
      createdAt: "2020-05-17T03:28:54.000Z",
      updatedAt: "2020-05-17T03:46:06.000Z"
    }
  ]
};

export default {
  name: "AdminCategories",
  components: {
    AdminNav
  },
  // 3. 定義 Vue 中使用的 data 資料
  data() {
    return {
      categories: [],
      newCategoryName: ""
    };
  },
  // 5. 調用 `fetchCategories` 方法
  created() {
    this.fetchCategories();
  },
  methods: {
    // 4. 定義 `fetchCategories` 方法，把 `dummyData` 帶入 Vue 物件
    fetchCategories() {
      // 在每一個 category 中都添加一個 isEditing 屬性
      this.categories = dummyData.categories.map(category => ({
        ...category,
        isEditing: false,
        nameCached: ""
      }));
    },
    createCategory() {
      // TODO: 透過 API 告知伺服器欲新增的餐廳類別...

      // 將新的類別添加到陣列中
      this.categories.push({
        id: uuidv4(),
        name: this.newCategoryName
      });

      // 清空原本欄位中的內容
      this.newCategoryName = "";
    },
    deleteCategory(categoryId) {
      // TODO: 透過 API 告知伺服器欲刪除的餐廳類別

      // 將該餐廳類別從陣列中移除
      this.categories = this.categories.filter(
        category => category.id !== categoryId
      );
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
    updateCategory({ categoryId, name }) {
      // TODO: 透過 API 去向伺服器更新餐廳類別名稱
      console.log("update category name", name);
      this.toggleIsEditing(categoryId);
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