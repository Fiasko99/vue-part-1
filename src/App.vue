<template>
  <div id="app">
    <div class="container">
      <h1>Todo application</h1>
      <hr>
      
      <transition name="slide-fade" mode="out-in">
        <router-view />
      </transition>

    </div>
  </div>
</template>

<script>

</script>

<style>
.container {
  text-align: center;
  width: 70%;
  margin-left: 15%;
}
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
