<template>
    <div>
      <div style="margin-bottom: 1rem">
        <h4>Movie title : {{ movie.title }}</h4>
        <p>
          Movie director : {{ movie.director }}
          Movie release : {{ movie.releaseDate }}
          Genre : {{ movie.genre }}
          Duration : {{ movie.duration }}
        </p>
        <button class="btn btn-primary" @click="handleSelect">Select</button>
      </div>
    </div>
</template>

<script>
export default {
  props: {
    movie: Object
  },

  methods : {
    handleSelect() {
      this.$emit('selectMovie',this.movie.id)
    }
  }
}
</script>

<style>
button {
  display: inline;
}
</style>
