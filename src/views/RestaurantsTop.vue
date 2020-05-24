<template>
  <div class="container py-5">
    <!-- 使用 NavTabs 元件 -->
    <NavTabs />
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
            <span class="badge badge-secondary">收藏數：{{restaurant.FavoritedUsers.length}}</span>
            <p class="card-text">{{restaurant.description}}</p>
            <router-link
              :to="{name: 'restaurant', params: {id: restaurant.id}}"
              class="btn btn-primary mr-2"
            >Show</router-link>
            <button
              type="button"
              class="btn btn-danger mr-2"
              v-if="restaurant.isFavorited"
              @click.stop.prevent="removeFavorite(restaurant)"
            >移除最愛</button>
            <button
              type="button"
              class="btn btn-primary"
              v-else
              @click.stop.prevent="addFavorite(restaurant)"
            >加到最愛</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavTabs from "./../components/NavTabs";

const dummyData = {
  restaurants: [
    {
      id: 5,
      name: "Mitchel Beatty",
      tel: "171-324-8413",
      address: "85408 Francisca Square",
      opening_hours: "08:00",
      description: "Aut cumque excepturi exercitationem libero volupta",
      image: "https://i.imgur.com/awJFBLn.jpg",
      viewCounts: 282,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-24T09:40:05.000Z",
      CategoryId: 3,
      FavoritedUsers: [
        {
          id: 92,
          name: "asdasd",
          email: "asdasd@asdasd.asdasd",
          password:
            "$2a$10$J4Z/hkxNtpZYM0mj/eCaM.bBRTtTC4yOwISf4d..ia9sdB0ym/9yO",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-08T17:38:03.000Z",
          updatedAt: "2020-03-08T17:38:03.000Z",
          Favorite: {
            UserId: 92,
            RestaurantId: 5,
            createdAt: "2020-03-09T06:09:07.000Z",
            updatedAt: "2020-03-09T06:09:07.000Z"
          }
        },
        {
          id: 232,
          name: "wbh",
          email: "ReadingExchange@163.com",
          password:
            "$2a$10$1h2OE3ZFUTR6Lr9bojp4ee2fxUBya/NpkwveJNxpe7h2JeFe6eb0a",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-25T15:53:23.000Z",
          updatedAt: "2020-03-25T15:53:23.000Z",
          Favorite: {
            UserId: 232,
            RestaurantId: 5,
            createdAt: "2020-03-27T03:30:47.000Z",
            updatedAt: "2020-03-27T03:30:47.000Z"
          }
        },
        {
          id: 322,
          name: "123",
          email: "123@123",
          password:
            "$2a$10$puJ.mSl6Xp6S0SByjQNjxe34k/TjTCHOQDh1yUnANo3U80xsarEf2",
          isAdmin: false,
          image: "https://i.imgur.com/dQq7Bvo.jpg",
          createdAt: "2020-04-07T08:23:03.000Z",
          updatedAt: "2020-04-07T15:29:59.000Z",
          Favorite: {
            UserId: 322,
            RestaurantId: 5,
            createdAt: "2020-04-07T15:31:35.000Z",
            updatedAt: "2020-04-07T15:31:35.000Z"
          }
        },
        {
          id: 332,
          name: "wishfree",
          email: "wishfree76@gmail.com",
          password:
            "$2a$10$11XZtbdnc5DK.sEJbpzvE.TTUs0UDFBM1rOKQ7jgp.pHHZrRExaH6",
          isAdmin: false,
          image: null,
          createdAt: "2020-04-09T00:42:29.000Z",
          updatedAt: "2020-04-09T00:42:29.000Z",
          Favorite: {
            UserId: 332,
            RestaurantId: 5,
            createdAt: "2020-04-09T00:45:33.000Z",
            updatedAt: "2020-04-09T00:45:33.000Z"
          }
        },
        {
          id: 392,
          name: "aa",
          email: "a@a.com",
          password:
            "$2a$10$nDlJ2N.4NuGxlcVgDImPl.leyanHhxm6hHaJHxTz6EdSH91RFjS32",
          isAdmin: false,
          image: null,
          createdAt: "2020-05-23T09:09:12.000Z",
          updatedAt: "2020-05-23T09:09:12.000Z",
          Favorite: {
            UserId: 392,
            RestaurantId: 5,
            createdAt: "2020-05-24T09:39:27.000Z",
            updatedAt: "2020-05-24T09:39:27.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 5
    },
    {
      id: 26,
      name: "Sarai Breitenberg",
      tel: "114-064-6388 x05451",
      address: "118 Cole Dale",
      opening_hours: "08:00",
      description: "Reiciendis et voluptatibus officiis magni enim qui",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=93.53330481196743",
      viewCounts: 3,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-04-11T04:57:17.000Z",
      CategoryId: 4,
      FavoritedUsers: [
        {
          id: 332,
          name: "wishfree",
          email: "wishfree76@gmail.com",
          password:
            "$2a$10$11XZtbdnc5DK.sEJbpzvE.TTUs0UDFBM1rOKQ7jgp.pHHZrRExaH6",
          isAdmin: false,
          image: null,
          createdAt: "2020-04-09T00:42:29.000Z",
          updatedAt: "2020-04-09T00:42:29.000Z",
          Favorite: {
            UserId: 332,
            RestaurantId: 26,
            createdAt: "2020-04-09T00:43:01.000Z",
            updatedAt: "2020-04-09T00:43:01.000Z"
          }
        },
        {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$NyaAtgRuHx3i7hHlnb5IXOC4Uk4.q1J1iQs3op.ymdCEh7.tOwcH2",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-21T09:59:58.000Z",
          Favorite: {
            UserId: 2,
            RestaurantId: 26,
            createdAt: "2020-04-17T04:35:49.000Z",
            updatedAt: "2020-04-17T04:35:49.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 2
    },
    {
      id: 13,
      name: "Mrs. Eileen Lockman",
      tel: "(597) 404-9974 x003",
      address: "383 Stroman Center",
      opening_hours: "08:00",
      description: "Vitae id incidunt animi qui sapiente perferendis i",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=54.950245749491145",
      viewCounts: 7,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-04-11T03:56:01.000Z",
      CategoryId: 2,
      FavoritedUsers: [
        {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$VHKmtPqbcUzK46qxLllqj.w506U2N2TObMmnpdlNG2CLZPa1xzuTi",
          isAdmin: false,
          image: "https://i.imgur.com/IaCnj2S.jpg",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T10:01:11.000Z",
          Favorite: {
            UserId: 3,
            RestaurantId: 13,
            createdAt: "2020-03-30T01:34:36.000Z",
            updatedAt: "2020-03-30T01:34:36.000Z"
          }
        },
        {
          id: 112,
          name: "測試",
          email: "123@example.com",
          password:
            "$2a$10$oJlwrpCT8jAC2Kamet775u3kNbd.SV85yvHH9c/L2bKODZ437Cn/K",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-12T15:28:49.000Z",
          updatedAt: "2020-03-12T15:28:49.000Z",
          Favorite: {
            UserId: 112,
            RestaurantId: 13,
            createdAt: "2020-04-20T09:19:19.000Z",
            updatedAt: "2020-04-20T09:19:19.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 2
    },
    {
      id: 9,
      name: "Luz Schaden",
      tel: "1-712-742-4184",
      address: "4929 Wisozk Centers",
      opening_hours: "08:00",
      description: "Culpa deserunt molestiae eligendi est ex incidunt.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=6.497835218728576",
      viewCounts: 32,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-24T13:51:34.000Z",
      CategoryId: 5,
      FavoritedUsers: [
        {
          id: 92,
          name: "asdasd",
          email: "asdasd@asdasd.asdasd",
          password:
            "$2a$10$J4Z/hkxNtpZYM0mj/eCaM.bBRTtTC4yOwISf4d..ia9sdB0ym/9yO",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-08T17:38:03.000Z",
          updatedAt: "2020-03-08T17:38:03.000Z",
          Favorite: {
            UserId: 92,
            RestaurantId: 9,
            createdAt: "2020-03-09T06:09:12.000Z",
            updatedAt: "2020-03-09T06:09:12.000Z"
          }
        },
        {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$NyaAtgRuHx3i7hHlnb5IXOC4Uk4.q1J1iQs3op.ymdCEh7.tOwcH2",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-21T09:59:58.000Z",
          Favorite: {
            UserId: 2,
            RestaurantId: 9,
            createdAt: "2020-03-24T08:51:28.000Z",
            updatedAt: "2020-03-24T08:51:28.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 2
    },
    {
      id: 7,
      name: "Miss Letitia Will",
      tel: "(770) 750-6811 x99988",
      address: "8145 Laisha Keys",
      opening_hours: "08:00",
      description: "Aut earum molestiae et ducimus adipisci ut maxime.",
      image: "https://i.imgur.com/50clDpn.jpg",
      viewCounts: 100,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-24T13:56:16.000Z",
      CategoryId: 5,
      FavoritedUsers: [
        {
          id: 92,
          name: "asdasd",
          email: "asdasd@asdasd.asdasd",
          password:
            "$2a$10$J4Z/hkxNtpZYM0mj/eCaM.bBRTtTC4yOwISf4d..ia9sdB0ym/9yO",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-08T17:38:03.000Z",
          updatedAt: "2020-03-08T17:38:03.000Z",
          Favorite: {
            UserId: 92,
            RestaurantId: 7,
            createdAt: "2020-03-09T06:09:10.000Z",
            updatedAt: "2020-03-09T06:09:10.000Z"
          }
        },
        {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z",
          Favorite: {
            UserId: 1,
            RestaurantId: 7,
            createdAt: "2020-05-24T04:08:55.000Z",
            updatedAt: "2020-05-24T04:08:55.000Z"
          }
        }
      ],
      isFavorited: true,
      FavoriteCount: 2
    },
    {
      id: 6,
      name: "Vicenta Gutkowski Test By Nacho",
      tel: "128-905-3953",
      address: "371 Reuben Vista test",
      opening_hours: "00:00",
      description: "labore",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=16.659471621888123",
      viewCounts: 86,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-24T13:50:35.000Z",
      CategoryId: 2,
      FavoritedUsers: [
        {
          id: 92,
          name: "asdasd",
          email: "asdasd@asdasd.asdasd",
          password:
            "$2a$10$J4Z/hkxNtpZYM0mj/eCaM.bBRTtTC4yOwISf4d..ia9sdB0ym/9yO",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-08T17:38:03.000Z",
          updatedAt: "2020-03-08T17:38:03.000Z",
          Favorite: {
            UserId: 92,
            RestaurantId: 6,
            createdAt: "2020-03-09T06:09:10.000Z",
            updatedAt: "2020-03-09T06:09:10.000Z"
          }
        },
        {
          id: 2,
          name: "user1",
          email: "user1@example.com",
          password:
            "$2a$10$NyaAtgRuHx3i7hHlnb5IXOC4Uk4.q1J1iQs3op.ymdCEh7.tOwcH2",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-21T09:59:58.000Z",
          Favorite: {
            UserId: 2,
            RestaurantId: 6,
            createdAt: "2020-04-17T03:27:36.000Z",
            updatedAt: "2020-04-17T03:27:36.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 2
    },
    {
      id: 11,
      name: "Vergie Considine",
      tel: "351.951.8030 x0330",
      address: "8865 Conrad Mill",
      opening_hours: "08:00",
      description: "Quia omnis natus est praesentium dolores aliquid d",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=0.7508871784973614",
      viewCounts: 5,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-24T13:56:10.000Z",
      CategoryId: 5,
      FavoritedUsers: [
        {
          id: 92,
          name: "asdasd",
          email: "asdasd@asdasd.asdasd",
          password:
            "$2a$10$J4Z/hkxNtpZYM0mj/eCaM.bBRTtTC4yOwISf4d..ia9sdB0ym/9yO",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-08T17:38:03.000Z",
          updatedAt: "2020-03-08T17:38:03.000Z",
          Favorite: {
            UserId: 92,
            RestaurantId: 11,
            createdAt: "2020-03-09T06:09:13.000Z",
            updatedAt: "2020-03-09T06:09:13.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 1
    },
    {
      id: 10,
      name: "Corbin Gusikowski",
      tel: "(506) 198-3977",
      address: "4747 Lubowitz Brook",
      opening_hours: "08:00",
      description: "Aut quia aut ea nostrum quae doloremque necessitat",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=6.84802493817025",
      viewCounts: 36,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-05-24T13:54:17.000Z",
      CategoryId: 5,
      FavoritedUsers: [
        {
          id: 92,
          name: "asdasd",
          email: "asdasd@asdasd.asdasd",
          password:
            "$2a$10$J4Z/hkxNtpZYM0mj/eCaM.bBRTtTC4yOwISf4d..ia9sdB0ym/9yO",
          isAdmin: false,
          image: null,
          createdAt: "2020-03-08T17:38:03.000Z",
          updatedAt: "2020-03-08T17:38:03.000Z",
          Favorite: {
            UserId: 92,
            RestaurantId: 10,
            createdAt: "2020-03-09T06:09:12.000Z",
            updatedAt: "2020-03-09T06:09:12.000Z"
          }
        }
      ],
      isFavorited: false,
      FavoriteCount: 1
    },
    {
      id: 44,
      name: "Madge Moen",
      tel: "794.584.3958 x1725",
      address: "6233 Annamae Mission",
      opening_hours: "08:00",
      description: "sed ut illum",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=33.163077027772346",
      viewCounts: 0,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z",
      CategoryId: 3,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0
    },
    {
      id: 43,
      name: "Mrs. Noemy Watsica",
      tel: "(252) 981-9430 x3227",
      address: "1218 Dariana Ports",
      opening_hours: "08:00",
      description: "Animi rerum suscipit iusto id autem et. Facilis id",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=23.889387774329695",
      viewCounts: 0,
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z",
      CategoryId: 5,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0
    }
  ]
};

export default {
  name: "RestaurantsTop",
  components: {
    NavTabs
  },
  data() {
    return {
      restaurants: []
    };
  },
  created() {
    this.fetchTopRestaurants();
  },
  methods: {
    fetchTopRestaurants() {
      const { restaurants } = dummyData;
      this.restaurants = restaurants;
    },
    addFavorite(restaurant) {
      restaurant.isFavorited = true;
    },
    removeFavorite(restaurant) {
      restaurant.isFavorited = false;
    }
  }
};
</script>