<template>
  <div class="hello">
    <p></p>

    <div class="card text-center m-3">
      <h3 class="card-header">Les listes nom des Pays</h3>
      <div class="card-body">
        <table class="table table-striped"> 
          <thead class="thead-dark">
            <tr>
              <th>Flag</th>
              <th>Name</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(pays, index) in pageOfItems" :key="index">
              <td><img :src="pays.flag" alt="" width="50px" height="50px"/></td>
              <td>{{ pays.name }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="card-footer pb-0 pt-3">
        <jw-pagination
          :pageSize="18"
          :items="pays"
          @changePage="onChangePage"
        ></jw-pagination>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import JwPagination from "jw-vue-pagination";

export default {
  name: "HelloWorld",
  components: {
    JwPagination,
  },
  data() {
    return {
      pays: null,
      pageOfItems: [],
    };
  },
  mounted() {
    axios.get("https://restcountries.eu/rest/v2/all").then((response) => {
      this.pays = response.data;
      console.log(this.pays);
    });
  },
  methods: {
    onChangePage(pageOfItems) {
      console.log(pageOfItems);

      this.pageOfItems = pageOfItems;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
