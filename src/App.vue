<template>
  <div id="app">
    <navigation></navigation>
      <transition name="slide-left" mode="out-in">
        <keep-alive>
          <router-view :key="$route.fullPath" class="child-view" />
        </keep-alive>
      </transition>
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

<style scoped>
.child-view {
  transition: all .2s cubic-bezier(.55,0,.1,1);
}
.slide-left-enter, .slide-right-leave-active {
  opacity: 0;
  -webkit-transform: translate(30px, 0);
  transform: translate(30px, 0);
}
.slide-left-leave-active, .slide-right-enter {
  opacity: 0;
  -webkit-transform: translate(-30px, 0);
  transform: translate(-30px, 0);
}
</style>
