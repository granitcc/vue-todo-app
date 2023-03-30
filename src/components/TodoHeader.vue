<template>
  <header>
    <nav class="container">
      <div class="branding">
        <h1>Todos Creator</h1>
      </div>
      <ul class="nav-routes">
        <li><RouterLink to="/">Home</RouterLink></li>
        <li><RouterLink to="/about">About</RouterLink></li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { RouterLink } from "vue-router";
</script>

<style lang="scss" scoped>
header {
  background-color: #bdd6be;
  nav {
    display: flex;
    align-items: center;
    padding: 25px 16px;
    .branding {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        max-width: 50px;
      }
      h1 {
        font-size: 24px;
      }
    }
    .nav-routes {
      display: flex;
      flex: 1;
      justify-content: flex-end;
      gap: 12px;
      list-style: none;
      a {
        text-decoration: none;
        color: inherit;
        &:hover {
          color: rgb(244, 244, 244);
          text-decoration: underline;
        }
      }
    }
  }
}
</style>
