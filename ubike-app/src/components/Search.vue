<template>
  <div id="searchBar">
    <p>站點名稱搜尋: <input type="text" v-model="searchName" /></p>
  </div>
</template>

<script>
export default {
  props: {
    //parentMessage: String
  },
  data() {
    return {
      searchName: "",
    };
  },
  watch: {
    searchName() {
      console.log("search");
      this.$emit("search", this.searchName);
    },
  },
};
</script>

<style>
#searchBar{
  text-align :left;
  margin-left :20px;
}
</style>
