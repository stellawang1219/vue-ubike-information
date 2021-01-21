<template>
  <div id="app">
    <h1>YouBike 臺北市公共自行車即時資訊</h1>
    <Search @search="search"></Search>
    <UbikeTable :resultList="splitedStops" @sort="setSort"> </UbikeTable>
    <Pagination
      :currentPage="currentPage"
      :totalPage="totalPage"
      @setPage="setPage"
    ></Pagination>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import UbikeTable from "./components/UbikeTable.vue";
import Pagination from "./components/PaginationNav.vue";

export default {
  name: "App",
  components: {
    Search,
    UbikeTable,
    Pagination,
  },
  data() {
    return {
      ubikeStops: [],
      searchName: "",
      currentSortType: "",
      isAsc: false,
      countOfPage: 20,
      currentPage: 1,
    };
  },
  computed: {
    filteredStops() {
      return this.ubikeStops.filter((s) => s.sna.includes(this.searchName));
    },
    sortedStops() {
      const sortedList = [...this.filteredStops];
      if (this.isAsc) {
        return sortedList.sort(
          (a, b) => a[this.currentSortType] - b[this.currentSortType]
        );
      } else {
        return sortedList.sort(
          (a, b) => b[this.currentSortType] - a[this.currentSortType]
        );
      }
    },
    splitedStops() {
      const pageStart = this.countOfPage * (this.currentPage - 1);
      const pageEnd = pageStart + this.countOfPage;
      //console.log("splitedStops,"+pageStart +","+pageEnd);
      return this.sortedStops.slice(pageStart, pageEnd);
    },
    totalPage() {
      return Math.ceil(this.sortedStops.length / this.countOfPage);
    },
  },
  methods: {
    setSort(val) {
      //console.log("setSort:" + val.target+","+val.isAsc);
      this.currentSortType = val.target;
      this.isAsc = val.isAsc;
    },
    setPage(page) {
      //console.log("setPage:"+page);
      if (page < 1 || page > this.totalPage) {
        return;
      }
      this.currentPage = page;
    },
    search(val) {
      console.log("Father_search:" + val);
      this.searchName = val;
    },
  },
  watch: {
    // uBikeStops(val) {
    //   console.log(val);
    // },
    filteredStops(){
      this.setPage(1);
    }
  },
  created() {
    fetch("https://tcgbusfs.blob.core.windows.net/blobyoubike/YouBikeTP.gz")
      .then((res) => res.json())
      .then((res) => {
        this.ubikeStops = Object.keys(res.retVal).map((key) => res.retVal[key]);
      });
  },
};
</script>
"
<style lang="scss">
@import "https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css";
@import "https://pro.fontawesome.com/releases/v5.10.0/css/all.css";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
