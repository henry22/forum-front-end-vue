<template>
  <div class="container py-5">
    <h1>餐廳描述頁</h1>
    <!-- 餐廳資訊頁 RestaurantDetail -->
    <RestaurantDetail :initial-restaurant="restaurant" />
    <hr />
    <!-- 餐廳評論 RestaurantComments -->
    <!-- 新增評論 CreateComment -->
  </div>
</template>

<script>
import RestaurantDetail from './../components/RestaurantDetail'

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
    viewCounts: 277,
    createdAt: "2020-02-28T14:38:32.000Z",
    updatedAt: "2020-05-24T06:49:58.565Z",
    CategoryId: 3,
    Category: {
      id: 3,
      name: "義大利料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
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
      }
    ],
    LikedUsers: [
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
        Like: {
          UserId: 232,
          RestaurantId: 5,
          createdAt: "2020-03-27T03:30:48.000Z",
          updatedAt: "2020-03-27T03:30:48.000Z"
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
        Like: {
          UserId: 322,
          RestaurantId: 5,
          createdAt: "2020-04-07T15:31:36.000Z",
          updatedAt: "2020-04-07T15:31:36.000Z"
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
        Like: {
          UserId: 2,
          RestaurantId: 5,
          createdAt: "2020-04-17T04:26:51.000Z",
          updatedAt: "2020-04-17T04:26:51.000Z"
        }
      },
      {
        id: 1,
        name: "root",
        email: "root@example.com",
        password:
          "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
        isAdmin: true,
        image: null,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-03-02T17:09:40.000Z",
        Like: {
          UserId: 1,
          RestaurantId: 5,
          createdAt: "2020-05-24T04:11:51.000Z",
          updatedAt: "2020-05-24T04:11:51.000Z"
        }
      }
    ],
    Comments: [
      {
        id: 5,
        text: "Et est asperiores eaque accusantium voluptas.",
        UserId: 3,
        RestaurantId: 5,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        User: {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$VHKmtPqbcUzK46qxLllqj.w506U2N2TObMmnpdlNG2CLZPa1xzuTi",
          isAdmin: true,
          image: "https://i.imgur.com/IaCnj2S.jpg",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-21T09:44:01.000Z"
        }
      },
      {
        id: 55,
        text: "Eos facilis facere debitis nam.",
        UserId: 3,
        RestaurantId: 5,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        User: {
          id: 3,
          name: "user2",
          email: "user2@example.com",
          password:
            "$2a$10$VHKmtPqbcUzK46qxLllqj.w506U2N2TObMmnpdlNG2CLZPa1xzuTi",
          isAdmin: true,
          image: "https://i.imgur.com/IaCnj2S.jpg",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-04-21T09:44:01.000Z"
        }
      },
      {
        id: 105,
        text: "Rerum rerum quaerat voluptatem.",
        UserId: 1,
        RestaurantId: 5,
        createdAt: "2020-02-28T14:38:32.000Z",
        updatedAt: "2020-02-28T14:38:32.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-02T17:09:40.000Z"
        }
      },
      {
        id: 4232,
        text: "hellow world",
        UserId: 1,
        RestaurantId: 5,
        createdAt: "2020-04-01T10:35:34.000Z",
        updatedAt: "2020-04-01T10:35:34.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-02T17:09:40.000Z"
        }
      },
      {
        id: 4242,
        text: "test test",
        UserId: 1,
        RestaurantId: 5,
        createdAt: "2020-04-01T10:37:25.000Z",
        updatedAt: "2020-04-01T10:37:25.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-02T17:09:40.000Z"
        }
      },
      {
        id: 4282,
        text: "delicious",
        UserId: 1,
        RestaurantId: 5,
        createdAt: "2020-04-06T13:54:12.000Z",
        updatedAt: "2020-04-06T13:54:12.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-02T17:09:40.000Z"
        }
      },
      {
        id: 4362,
        text: "12",
        UserId: 322,
        RestaurantId: 5,
        createdAt: "2020-04-07T15:32:04.000Z",
        updatedAt: "2020-04-07T15:32:04.000Z",
        User: {
          id: 322,
          name: "123",
          email: "123@123",
          password:
            "$2a$10$puJ.mSl6Xp6S0SByjQNjxe34k/TjTCHOQDh1yUnANo3U80xsarEf2",
          isAdmin: false,
          image: "https://i.imgur.com/dQq7Bvo.jpg",
          createdAt: "2020-04-07T08:23:03.000Z",
          updatedAt: "2020-04-07T15:29:59.000Z"
        }
      },
      {
        id: 4372,
        text: "123",
        UserId: 1,
        RestaurantId: 5,
        createdAt: "2020-04-08T09:55:40.000Z",
        updatedAt: "2020-04-08T09:55:40.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$J9pLpJJ1Tzfe/ZcjdYwXdumyh.3F5E.w/HTxRcH./cl3azhgekgQe",
          isAdmin: true,
          image: null,
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-03-02T17:09:40.000Z"
        }
      },
      {
        id: 4442,
        text: "hi",
        UserId: 352,
        RestaurantId: 5,
        createdAt: "2020-04-13T07:30:36.000Z",
        updatedAt: "2020-04-13T07:30:36.000Z",
        User: {
          id: 352,
          name: "my",
          email: "myname@name.name",
          password:
            "$2a$10$nHaozM7WZpf2GplWHg05RezJgoX2q8371l3RyYWL7Mi6cOAWsO1Ou",
          isAdmin: false,
          image: null,
          createdAt: "2020-04-13T07:30:19.000Z",
          updatedAt: "2020-04-13T07:30:19.000Z"
        }
      }
    ]
  },
  isFavorited: false,
  isLiked: true
};
export default {
  components: {
    RestaurantDetail
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryName: "",
        image: "",
        openingHours: "",
        tel: "",
        address: "",
        description: "",
        isFavorited: false,
        isLiked: false
      },
      restaurantComments: []
    };
  },
  created() {
    const {id: restaurantId} = this.$route.params
    this.fetchRestaurant(restaurantId)
  },
  methods: {
    fetchRestaurant(restaurantId) {
      console.log('fetchRestaurant id: ', restaurantId)

      const { restaurant, isFavorited, isLiked } = dummyData;
      const {
        id,
        name,
        Category,
        image,
        opening_hours,
        tel,
        address,
        description,
        Comments
      } = restaurant;
      this.restaurant = {
        id,
        name,
        categoryName: Category ? Category.name : '未分類',
        image,
        openingHours: opening_hours,
        tel,
        address,
        description,
        isFavorited,
        isLiked
      }
      this.restaurantComments = Comments
    }
  }
};
</script>