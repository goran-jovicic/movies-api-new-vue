<template>
  <div>
    <MovieSearch @searchTermUpdated="setSearchTerm"></MovieSearch>
    <ul>
      <li v-for="(movie, index) in filteredMovies" :key="index">
        <MovieRow :movie="movie"></MovieRow>
      </li>
    </ul>
  </div>
</template>

<script>
import { moviesService } from "../services/MoviesService";
import MovieRow from "./MovieRow";
import MovieSearch from "./MovieSearch";

export default {
  components: {
    MovieRow,
    MovieSearch
  },

  data() {
    return {
      movies: [],
      term: ""
    };
  },

  beforeRouteEnter(to, from, next) {
    next(vm => {
      moviesService.getAll().then(response => {
        vm.movies = response.data;
      });
    });
  },

  methods : {
    setSearchTerm(term) {
      this.term = term
    }
  },

  computed: {
    filteredMovies() {
      return this.movies.filter(movie => {
        return movie.title
          .toLowerCase()
          .includes(this.term.toLowerCase());
      });
    }
  }
};
</script>

<style>
li {
  list-style: none;
}
</style>
