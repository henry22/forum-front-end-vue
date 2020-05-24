<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <!-- 前一頁 previousPage -->
      <li :class="['page-item', {disabled: currentPage === 1}]" v-show="previousPage">
        <router-link
          class="page-link"
          aria-label="Previous"
          :to="{name: 'restaurants', query: {categoryId, page: previousPage}}"
        >
          <span aria-hidden="true">&laquo;</span>
        </router-link>
      </li>
      <!-- 頁碼 -->
      <li
        :class="['page-item', {active: currentPage === page}]"
        v-for="page in totalPage"
        :key="page"
      >
        <router-link
          class="page-link"
          :to="{name: 'restaurants', query: {categoryId, page}}"
        >{{page}}</router-link>
      </li>
      <!-- 後一頁 nextPage -->
      <li :class="['page-item', {disabled: currentPage === totalPage.length}]" v-show="nextPage">
        <router-link
          class="page-link"
          aria-label="Next"
          :to="{name: 'restaurants', query: {categoryId, page: nextPage}}"
        >
          <span aria-hidden="true">&raquo;</span>
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    categoryId: {
      type: [Number, String],
      default: ''
    },
    currentPage: {
      type: Number,
      default: 1
    },
    totalPage: {
      type: Array,
      required: true
    },
    previousPage: {
      type: Number,
      required: true
    },
    nextPage: {
      type: Number,
      required: true
    }
  }
};
</script>