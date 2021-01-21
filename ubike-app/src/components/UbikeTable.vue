<template>
  <table class="table table-striped">
      <thead>
        <tr>
          <th>
            <a href="#" @click.prevent="setSort('sno')">
              #
              <i class="fa fa-sort-up" aria-hidden="true"></i>
              <i class="fa fa-sort-down" aria-hidden="true"></i>
            </a>
          </th>
          <th>場站名稱</th>
          <th>場站區域</th>
          <th>
            <a href="#" @click.prevent="setSort('sbi')">
              目前可用車輛
              <i class="fa fa-sort-up" aria-hidden="true"></i>
              <i class="fa fa-sort-down" aria-hidden="true"></i>
            </a>
          </th>
          <th>
            <a href="#" @click.prevent="setSort('tot')">
              總停車格
              <i class="fa fa-sort-up" aria-hidden="true"></i>
              <i class="fa fa-sort-down" aria-hidden="true"></i>
            </a>
          </th>
          <th>資料更新時間</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="s in resultList" :key="s.sno">
          <td>{{ s.sno }}</td>
          <td>{{ s.sna }}</td>
          <td>{{ s.sarea }}</td>
          <td>{{ s.sbi }}</td>
          <td>{{ s.tot }}</td>
          <td>{{ timeFormat(s.mday) }}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
</template>

<script>
export default {
  props: {
    resultList: Object,
  },
  data(){
    return{
      //currentSortType: '',
      isAsc: false,
    }
  },
   methods: {
     timeFormat(t) {
          var date = [], time = [];
          date.push(t.substr(0, 4));
          date.push(t.substr(4, 2));
          date.push(t.substr(6, 2));
          time.push(t.substr(8, 2));
          time.push(t.substr(10, 2));
          time.push(t.substr(12, 2));
          return date.join("/") + ' ' + time.join(":");
        },
      setSort(target) {
        this.isAsc = !this.isAsc;
        this.$emit('sort', {target:target,isAsc:!this.isAsc});
      },
   },
}
</script>

