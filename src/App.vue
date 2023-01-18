<template>
  <AppHeader></AppHeader>
  <main class="container">
    <router-view></router-view>
  </main>
  
</template>
<script>
import AppHeader from './components/AppHeader.vue';
  export default {
    name: 'App',
    components:{
      AppHeader
    }
    
  }
</script>

<style lang="scss" scoped>
</style>