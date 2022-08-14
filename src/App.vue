<template>
  <div id="nav" class="p-14 bg-green-200">
    <router-link class="flex justify-center text-4xl text-yellow-700" to="/">Pokemon Picker</router-link>
  </div>
  <router-view></router-view>
</template>

<style>
html{
  height: 100%;
}
body{
  margin: 0;
  padding: 0;
  height: 100%;
}
#app{
  height: 100%;
}
</style>