<template>
  <div class="overflow-auto">
    <p class="mt-3">Current Page: {{ currentPage }}</p>
    <b-table id="my-table" :items="items" :per-page="perPage" :current-page="currentPage" small></b-table>
    <b-pagination
      :total-rows="rows"
      v-model="currentPage"
      :per-page="perPage"
      aria-controls="my-table"
    ></b-pagination>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      perPage: 10,
      currentPage: 1,
      items: []
    };
  },
  computed: {
    rows() {
      return this.items.length;
    }
  },
  mounted() {
    axios.get("http://starlord.hackerearth.com/bankAccount").then(response => {
      console.log(response.data);
      this.items = response.data;
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
