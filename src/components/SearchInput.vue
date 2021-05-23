<template>
  <div class="input">
    <b-form-input v-model="text" placeholder="Enter movie name"></b-form-input>
  </div>
</template>

<script>
export default {
  name: "SearchInput",
  data() {
    return {
      text: "",
      url: "http://www.omdbapi.com/?i=tt3896198&apikey=f68f2cab",
    };
  },
  mounted() {
    this.axios.get(this.url);
  },
};
</script>

<style lang="scss" scoped>
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

.input {
  max-width: 300px;
}
</style>
