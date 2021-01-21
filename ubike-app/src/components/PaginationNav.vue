<template>
  <div>
    <nav aria-label="...">
      <ul class="pagination">
        <li class="page-item" :class="{ disabled: currentPage - 1 == 0 }">
          <a class="page-link" href="#" @click="setPage(currentPage - 1)">
            Previous
          </a>
        </li>
        <li
          class="page-item"
          :class="{ active: page === currentPage }"
          v-for="page of totalPage"
          :key="page"
        >
          <a class="page-link" href="#" @click="setPage(page)">{{ page }}</a>
        </li>
        <li class="page-item" :class="{ disabled: currentPage == totalPage }">
          <a class="page-link" href="#" @click="setPage(currentPage + 1)">
            Next
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: Number,
    totalPage: Number,
  },
  methods: {
    setPage(page) {
      //console.log("SetPage:"+page);
      this.$emit("setPage", page);
    },
  },
};
</script>
