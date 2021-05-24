<template>
  <div class="main">
    <div class="input-wrap">
      <label for="search">Movie name:</label>
      <b-form-input
        v-model="movieName"
        placeholder="Enter movie name"
        debounce="1000"
        id="search"
      ></b-form-input>
    </div>
    <div class="input-wrap">
      <label for="year">Year:</label>
      <b-form-input v-model="year" placeholder="year" id="year"></b-form-input>
    </div>
    <div class="input-wrap">
      <label for="type">Type:</label>
      <b-form-select
        v-model="type"
        :options="typeOptions"
        id="type"
      ></b-form-select>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchInput",
  data() {
    return {
      movieName: "",
      year: "",
      type: "",
      typeOptions: ["movie", "series", "episode"],
      baseUrl: "http://www.omdbapi.com/?i=tt3896198&apikey=f68f2cab",
    };
  },
  computed: {
    url() {
      return (
        this.baseUrl +
        `&t=${this.movieName}` +
        `&y=${this.year}` +
        `&type=${this.type}`
      );
    },
  },
  methods: {
    async getMovie() {
      const data = await this.axios.get(this.url);
      console.log(data, "data");
    },
  },
  watch: {
    movieName(newValue) {
      if (newValue) this.getMovie();
    },
  },
};
</script>

<style lang="scss" scoped>
.main {
  display: flex;
}

.input-wrap {
  display: flex;
  align-items: center;

  label {
    white-space: nowrap;
    margin-left: 1rem;
    margin-right: 0.5rem;
    margin-bottom: 0;
  }
}
</style>
