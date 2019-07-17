<template>
  <div>
    <div>
      <hr>
      <MovieSearch @searchTermUpdated="setSearchTerm"></MovieSearch>
      <hr>
    </div>
    <div>
      <button @click="selectAll">Select all </button>
      <button @click="deselectAll">Deselect all </button>
      <hr>
    </div>
    <div>
      <button @click="sortByNameAsc">Sort by name asc</button>
      <button @click="sortByNameDesc">Sort by name desc</button>
      <button @click="sortByDurAsc">Sort by duration asc</button>
      <button @click="sortByDurDesc">Sort by duration desc</button>
    </div>
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
    },

    selectAll(){
      this.selectedList = this.filteredMovies.map(filteredMovie => filteredMovie.id)
    },

    deselectAll(){
      this.selectedList = [];
    },

    sortByNameAsc() {
      
    },

    sortByNameDesc() {

    },

    sortByDurAsc(){

    },

    sortByDurDesc(){

    }
  },

  computed: {
    filteredMovies() {
      return this.movies.filter(movie => {
          return movie.title.toLowerCase().includes(this.term.toLowerCase())
      });
    },
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
