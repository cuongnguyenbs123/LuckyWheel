<template>
    <div class="sticky-row">
        <div class="higt-score">
            <router-link to="/">
                <img
                    src="@/assets/images/leaderboard.15d560d6.webp"
                    class="higt-score-icon"
                    alt=""
                />
            </router-link>
        </div>
        <div class="play-more">
            <div class="btn-more">
                <router-link to="/">
                    <img
                        src="@/assets/images/games.33b0ee87.webp"
                        class="play-more-icon"
                        alt=""
                    />
                    Play more games
                </router-link>
            </div>
        </div>
         <div class="rewards">
            <router-link to="/">
                <img
                    src="@/assets/images/rewards.3b52607e.webp"
                    class="rewards-icon"
                    alt=""
                />
            </router-link>
        </div>
    </div>
</template>

<script>

export default {};
</script>

<style scoped>
@import url("@/assets/css/stickyrow.css");
</style>
