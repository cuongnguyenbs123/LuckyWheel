<template>
    <div class="wrapper">
        <div class="spin">
            <div class="row">
                <h3>☆Lucky Wheel☆</h3>
            </div>
            <div class="row">
                <p class="hpPoint">
                    <img
                        src="https://yowin.fun/img/hpoint.7397a144.webp"
                        alt=""
                    />
                </p>
            </div>
            <div class="wheel-container row">
                <img
                    src="@/assets/images/wheel.ed1e9675.webp"
                    class="rotary"
                    :class="{ freeze: freeze }"
                    :style="`transform: rotate(${wheelDeg}deg)`"
                    alt=""
                />
                <img
                    src="https://yowin.fun/img/front.9f26e2ea.webp"
                    class="arrow"
                    alt=""
                    @click="Onrolling()"
                />
            </div>
            <the-sticky-row />
        </div>
    </div>
</template>

<script>
import TheStickyRow from "@/components/TheStickyRow.vue";
export default {
    name: "HomeView",
    components: { TheStickyRow },
     created() {
           this.chosenPrizeList = this.prizeListOrigin
        },
    methods: {
        Onrolling() {
            if (this.rolling) return;
            const result = Math.floor(
                Math.random() * this.chosenPrizeList.length
            );
            this.roll(result);
        },
        roll(result) {
            this.rolling = true;
            this.rol = (this.wheelDeg % 360) +6 * 360 +(360 / this.chosenPrizeList.length) * result
            this.wheelDeg =this.wheelDeg - (this.wheelDeg % 360) +6 * 360 +(360 / this.chosenPrizeList.length) * result;
            setTimeout(() => {
                this.rolling = false;
                alert("Result：" + this.chosenPrizeList[result].name);
            }, 4500);
        },
    },
    data() {
        return {
            freeze: false,
            rolling: false,
            rol:0,
            wheelDeg: 0,
            prizeListOrigin: [
                {
                   name: "P.Code",
                     percent: 20/360*100,
                },
                {
                    name: "20$",
                    percent: 20/360*100,
                },
                {
                    name: "P.Code",
                     percent: 20/360*100,
                },
                {
                    name: "XiaoMi",
                     percent: 20/360*100,
                },
                {
                    name: "P.Code",
                      percent: 20/360*100,
                },
                {
                    name: "SJC",
                     percent: 20/360*100,
                },
                {
                    name: "P.Code",
                      percent: 20/360*100,
                },
                  {
                    name: "SamSung Note 20",
                      percent: 20/360*100,
                },
                  {
                    name: "P.Code",
                     percent: 20/360*100,
                },
                  {
                    name: "10$",
                     percent: 20/360*100,
                },
                  {
                    name: "P.Codes",
                     percent: 20/360*100,
                },
                  {
                    name: "5$",
                     percent: 20/360*100,
                },
                  {
                    name: "P.Code",
                     percent: 20/360*100,
                },
                  {
                    name: "2$",
                     percent: 20/360*100,
                },
                  {
                    name: "P.Code",
                      percent: 20/360*100,
                },
                  {
                    name: "1$",
                     percent: 20/360*100,
                },
                  {
                    name: "P.Code",
                     percent: 20/360*100,
                },
                  {
                    name: "5$",
                    percent: 20/360*100,
                },
            ],
        };
    },
};
</script>
<style scoped>
@import url("@/assets/css/body.css");
</style>
