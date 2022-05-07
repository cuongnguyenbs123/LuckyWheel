<template>
    <div class="header">
        <div class="header-content">
            <div class="left-header">
                <router-link to="/">
                    <div class="logo"></div>
                </router-link>
            </div>
            <div class="right-header">
                <div class="right-nav">
                    <div class="nav-item">
                        <router-link to="/">
                            <div class="nav-icon ticket"></div>
                            <div class="nav-point">0</div>
                        </router-link>
                    </div>
                    <div class="nav-item">
                        <router-link to="/">
                            <div class="nav-icon star"></div>
                            <div class="nav-point">0</div>
                        </router-link>
                    </div>
                    <div class="nav-item">
                        <router-link to="/">
                            <div class="nav-icon rank"></div>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
      
    },
};
</script>

<style scoped>
@import url("@/assets/css/header.css");
</style>
