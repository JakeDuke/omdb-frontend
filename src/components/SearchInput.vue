<template>
  <div class="main">
    <div class="inputs">
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
        <b-form-input
          v-model="year"
          placeholder="Year"
          id="year"
        ></b-form-input>
      </div>
      <div class="input-wrap">
        <label for="type">Type:</label>
        <b-form-select v-model="type" :options="typeOptions" id="type">
          <template #first>
            <b-form-select-option value=""
              >-- Please select type --</b-form-select-option
            >
          </template>
        </b-form-select>
      </div>
    </div>
    <div class="results">
      <b-table stacked :items="results">
        <template #cell(poster)="data">
          <img :src="data.item.Poster" alt="img" />
        </template>
        <template #cell(ratings)="data">
          <b-table stacked :items="data.item.Ratings"> </b-table>
        </template>
      </b-table>
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
      loading: null,
      results: [],
    };
  },
  computed: {
    url() {
      return (
        this.baseUrl +
        `&t=${this.movieName}` +
        `${this.year && `&y=${this.year}`}` +
        `${this.type && `&type=${this.type}`}`
      );
    },
  },
  methods: {
    async getMovie() {
      this.results = [];
      try {
        const { data } = await this.axios.get(this.url);
        this.results.push(data);
      } catch (e) {
        console.log(e);
      }
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
  display: block;
  width: 100%;
}
.inputs {
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

.results {
  width: 100%;
  overflow: auto;
}
</style>
