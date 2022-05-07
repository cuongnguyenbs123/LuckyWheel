<template>
    <div class="container">
        <the-header/>
        <router-view></router-view>
    </div>
</template>
<script>
/* eslint-disable */

import TheHeader from '@/components/TheHeader.vue';
export default {
  components: { TheHeader },
};
</script>
<style>
@import url("@/assets/css/main.css");
</style>
