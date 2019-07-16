<template>
  <div id="app">
    <nav class="navbar-brand">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/movies">Movies</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style>
</style>
