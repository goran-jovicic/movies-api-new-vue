<template>
  <div>
    <p>Search movies by title : </p>
    <input type="text" placeholder="Search.." v-model="searchTerm" v-on:input="handleSearch" />
    <button class="btn btn-primary" type="submit">Search</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: ""
    };
  },

  methods: {
    handleSearch() {
      this.$emit("searchTermUpdated", this.searchTerm);
    }
  }
};
</script>

<style>
</style>
