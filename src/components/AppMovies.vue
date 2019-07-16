<template>
  <div>
    <hr>
    <MovieSearch @searchTermUpdated="setSearchTerm"></MovieSearch>
    <hr>
    <button>Select all </button>
    <button>Deselect all </button>
    <ul>
      <li>Selected movie count : {{ selectedList.length }}</li>
      <li class="list-group-item list-group-item-danger" v-if="filteredMovies.length === 0 "> There is no movie with a title like that </li>
      <li v-for="(movie, index) in filteredMovies" :key="index">
        <MovieRow :movie="movie" @selectMovie="selectedMovies"></MovieRow>
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
      term: "",
      selectedList : []
    };
  },

  beforeRouteEnter(to, from, next) {
    next(vm => {
      moviesService.getAll().then(response => {
        vm.movies = response.data;
      });
    });
  },

  methods: {
    setSearchTerm(term) {
      this.term = term;
    },

    selectedMovies(movieId) {
      if(this.selectedList.includes(movieId)){
        return
      }
      this.selectedList.push(movieId)
    }
  },

  computed: {
    filteredMovies() {
      return this.movies.filter(movie => {
          return movie.title.toLowerCase().includes(this.term.toLowerCase())
      });
    }
  }
};
</script>

<style>
li {
  list-style: none;
}

body {
  margin : 1rem;
  text-align: center;
}
</style>
