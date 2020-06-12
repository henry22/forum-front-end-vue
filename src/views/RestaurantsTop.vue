<template>
  <div class="container py-5">
    <!-- 使用 NavTabs 元件 -->
    <NavTabs />

    <Spinner v-if="isLoading" />
    <template v-else>
      <h1 class="mt-5">人氣餐廳</h1>
      <hr />
      <div
        class="card mb-3"
        style="max-width: 540px;margin: auto;"
        v-for="restaurant in restaurants"
        :key="restaurant.id"
      >
        <div class="row no-gutters">
          <div class="col-md-4">
            <a href="#">
              <img
                class="card-img"
                src="https://loremflickr.com/320/240/food,dessert,restaurant/?random=2"
              />
            </a>
          </div>
          <div class="col-md-8">
            <div class="card-body">
              <h5 class="card-title">{{restaurant.name}}</h5>
              <span class="badge badge-secondary">收藏數：{{restaurant.FavoriteCount}}</span>
              <p class="card-text">{{restaurant.description}}</p>
              <router-link
                :to="{name: 'restaurant', params: {id: restaurant.id}}"
                class="btn btn-primary mr-2"
              >Show</router-link>
              <button
                type="button"
                class="btn btn-danger mr-2"
                v-if="restaurant.isFavorited"
                @click.stop.prevent="removeFavorite(restaurant.id)"
              >移除最愛</button>
              <button
                type="button"
                class="btn btn-primary"
                v-else
                @click.stop.prevent="addFavorite(restaurant.id)"
              >加到最愛</button>
            </div>
          </div>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";
import Spinner from "./../components/Spinner";
import restaurantsApi from "./../apis/restaurants";
import usersApi from "./../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  name: "RestaurantsTop",
  components: {
    NavTabs,
    Spinner
  },
  data() {
    return {
      restaurants: [],
      isLoading: true
    };
  },
  created() {
    this.fetchTopRestaurants();
  },
  methods: {
    async fetchTopRestaurants() {
      try {
        const { data } = await restaurantsApi.getTopRestaurants();

        this.restaurants = data.restaurants;

        this.isLoading = false;
      } catch (error) {
        console.log("error", error);
        this.isLoading = false;

        Toast.fire({
          icon: "error",
          title: "無法取得人氣餐廳資料，請稍後再試"
        });
      }
    },
    async addFavorite(restaurantId) {
      try {
        const { data } = await usersApi.addFavorite({ restaurantId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.restaurants = this.restaurants.map(restaurant => {
          if (restaurant.id !== restaurantId) {
            return restaurant;
          } else {
            return {
              ...restaurant,
              FavoriteCount: restaurant.FavoriteCount + 1,
              isFavorited: true
            };
          }
        });
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法加到最愛，請稍後再試"
        });
      }
    },
    async removeFavorite(restaurantId) {
      try {
        const { data } = await usersApi.deleteFavorite({ restaurantId });

        if (data.status !== "success") {
          throw new Error(data.message);
        }

        this.restaurants = this.restaurants.map(restaurant => {
          if (restaurant.id !== restaurantId) {
            return restaurant;
          } else {
            return {
              ...restaurant,
              FavoriteCount: restaurant.FavoriteCount - 1,
              isFavorited: false
            };
          }
        });
      } catch (error) {
        console.log("error", error);

        Toast.fire({
          icon: "error",
          title: "無法移除最愛，請稍後再試"
        });
      }
    }
  }
};
</script>