<template>
  <div class="container py-5">
    <div>
      <h1>{{restaurant.name}}</h1>
      <span class="badge badge-secondary mt-1 mb-3">{{restaurant.Category.name}}</span>
    </div>
    <hr />
    <ul>
      <li>評論數： {{ restaurant.Comments.length }}</li>
      <li>瀏覽次數： {{ restaurant.viewCounts }}</li>
    </ul>
    <button type="button" class="btn btn-link" @click="$router.back()">回上一頁</button>
  </div>
</template>

<script>
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
    viewCounts: 282,
    createdAt: "2020-02-28T14:38:32.000Z",
    updatedAt: "2020-05-24T09:40:05.000Z",
    CategoryId: 3,
    Category: {
      id: 3,
      name: "義大利料理",
      createdAt: "2020-02-28T14:38:32.000Z",
      updatedAt: "2020-02-28T14:38:32.000Z"
    },
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
          isAdmin: false,
          image: "https://i.imgur.com/IaCnj2S.jpg",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T10:01:11.000Z"
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
          isAdmin: false,
          image: "https://i.imgur.com/IaCnj2S.jpg",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T10:01:11.000Z"
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
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z"
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
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z"
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
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z"
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
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z"
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
          image: "https://i.imgur.com/kTEFFYJ.png",
          createdAt: "2020-02-28T14:38:32.000Z",
          updatedAt: "2020-05-24T14:57:48.000Z"
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
  }
};

export default {
  name: 'restaurant-dashboard',
  data() {
    return {
      restaurant: dummyData.restaurant
    }
  }
};
</script>