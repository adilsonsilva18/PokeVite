<script setup>
import { RouterLink, RouterView } from 'vue-router'
//import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <router-link class="navbar-brand" to="/">
        <img src="./assets/pikachu128.png" alt="" height="40" class="d-inline-block align-text-center">
        PokeVite
      </router-link>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" aria-current="page" href="/">Inicio</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/about">Sobre</a>
        </li>
        </ul>
    </div>
  </div>
</nav>

  <!-- CONTENT -->
  <router-view></router-view>
  <!-- -->

  <!-- FOOTER -->
  <footer class="bg-primary text-light">
    <div>
      Adilson {{ new Date().getFullYear() }} All Rights Reserved.
    </div>
  </footer>
  <!-- -->
</template>

<style>
footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  display: flex;
  align-items:center;
  justify-content: center;
  height: 56px;
}
</style>
