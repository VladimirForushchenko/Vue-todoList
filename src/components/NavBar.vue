<template>
  <nav class="blue darken-3">
    <div class="nav-wrapper blue darken-3">
      <router-link to="/" class="brand-logo">Tasks</router-link>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <router-link
        tag="li"
        to="/"
        exact
        active-class="active"
        >
        <a href="sass.html">Create</a>  
        </router-link>
        <router-link
        tag="li"
        to="/list"
        active-class="active"
        >
        <a href="sass.html">List</a>  
        </router-link>
      </ul>
    </div>
  </nav>

</template>

<script>
</script>

<style lang="scss" scoped>
  nav {
    padding: 0 2rem;
    position: fixed;
    top: 0;
  }
</style>