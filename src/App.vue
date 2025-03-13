<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { Header } from 'ant-design-vue/es/layout/layout'
</script>

<template>
  <Header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/entrar">Entrar</RouterLink>
        <RouterLink to="/cadastro">Cadastro</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </Header>

  <RouterView />
</template>

<style scoped>
@media (max-width: 1024px) {
  header {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .logo {
    width: 5rem;
    height: fit-content;
  }

  header .wrapper {
    flex-direction: column;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 1.5rem;
  }

  nav {
    font-size: 1rem;
  }
}
</style>
