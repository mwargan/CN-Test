<template>
  <div id="app">
    <navigation></navigation>
    <keep-alive>
      <router-view/>
    </keep-alive>
  </div>
</template>
<script>
import Navigation from './components/Nav.vue'

export default {
  components: {
    Navigation
  }
}
</script>
