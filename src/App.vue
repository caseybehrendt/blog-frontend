<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/posts">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!isLoggedIn" class="nav-link active" aria-current="page" to="/signup">
              Signup
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/post-new">New Post</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!isLoggedIn" class="nav-link active" aria-current="page" to="/login">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="isLoggedIn" class="nav-link active" aria-current="page" to="/logout">Logout</router-link>
          </li>
        </ul>
        <form class="d-flex">
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success" type="submit">Search</button>
        </form>
      </div>
    </div>
  </nav>
  <!-- <nav>
    <router-link to="/">Home</router-link>
    |
    <router-link to="/about">About</router-link>
    |
    <router-link to="/posts">Posts</router-link>
    |
    <router-link to="/signup">Signup</router-link>
    |
    <router-link to="/post-new">New Post</router-link>
    |
    <router-link to="/login">Login</router-link>
    |
    <router-link to="/logout">Logout</router-link>
  </nav> -->

  <router-view />
</template>
<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
    },
  },
};
</script>

<style>
body {
  font-family: Big Caslon, Book Antiqua, Palatino Linotype, Georgia, serif;
  background-image: url("https://www.pixeden.com/media/k2/galleries/220/001-wood-melamine-subttle-pattern-background-pat.jpg");
}
</style>
