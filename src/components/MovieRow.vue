<template>
    <div>
      <div>
        <h4>Movie title : {{ movie.title }}</h4>
        <p>Movie director : {{ movie.director }}</p>
        <p>Movie release : {{ movie.releaseDate }} </p>
        <p>Genre : {{ movie.genre }} </p>
        <p>Duration : {{ movie.duration }} </p>
      </div>
    </div>
</template>

<script>
export default {
  props: {
    movie: Object
  }
}
</script>

<style>

</style>
