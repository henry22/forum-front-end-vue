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
            <div class="category-name">{{category.name}}</div>
          </td>
          <td class="d-flex justify-content-between">
            <button type="button" class="btn btn-link mr-2">Edit</button>
            <button type="button" class="btn btn-link mr-2" @click.stop.prevent="deleteCategory(category.id)">Delete</button>
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
      this.categories = dummyData.categories;
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
      this.categories = this.categories.filter(category => category.id !== categoryId)
    }
  }
};
</script>