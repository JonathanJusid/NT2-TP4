<template>
  <div id="app" class="container-fluid mt-3">
    <div class="jumbotron">
      <h1>TP4 - NT2</h1>
      <br>
      <Navbar />
      <router-view></router-view>

    </div>
  </div>
</template>

<script>

import Navbar from './components/navbar'

export default {
  name: 'App',
  components: {
    Navbar,
  }
}
</script>

<style>

h1 {
  color: black;
}

.jumbotron {
  padding: 32px !important;
}

</style>

