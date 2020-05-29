<template>
  <div class="container py-5">
    <AdminRestaurantForm @after-submit="handleAfterSubmit" :initial-restaurant="restaurant" />
  </div>
</template>

<script>
import AdminRestaurantForm from "./../components/AdminRestaurantForm";

const dummyData = {
  restaurant: {
    id: 5,
    name: "Mitchel Beatty",
    tel: "171-324-8413",
    address: "85408 Francisca Square",
    opening_hours: "08:00",
    description:
      "Aut cumque excepturi exercitationem libero voluptates impedit. Enim animi repellendus tempora doloremque. Esse in delectus sequi ullam sed animi.",
    image: "https://i.imgur.com/awJFBLn.jpg",
    viewCounts: 284,
    createdAt: "2020-02-28T14:38:32.000Z",
    updatedAt: "2020-05-26T09:46:25.000Z",
    CategoryId: 3,
    Category: {
      id: 3,
      name: "義大利料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    }
  }
};

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
    fetchRestaurant(restaurantId) {
      console.log("fetchRestaurant id:", restaurantId);
      const { restaurant } = dummyData;
      const {
        id,
        name,
        categoryId,
        tel,
        address,
        description,
        image,
        opening_hours: openingHours
      } = restaurant;
      this.restaurant = {
        ...restaurant,
        id,
        name,
        categoryId,
        tel,
        address,
        description,
        image,
        openingHours
      };
    }
  }
};
</script>