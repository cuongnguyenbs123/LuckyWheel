<template>
    <div class="wrapper">
        <div class="wheel-history">
            <div class="history-title">
                <h5>Lịch sử quà tặng</h5>
            </div>
            <div class="history-content">
                <div
                    class="content"
                    v-for="(item, index) in prizeHistory"
                    :key="index"
                >
                    {{ item.name }}
                </div>
            </div>
        </div>
        <div class="spin">
            <div class="row">
                <h3>☆Lucky Wheel☆</h3>
            </div>
            <div class="row">
                <p class="hpPoint" v-if="lives > 0">
                    <img
                        v-for="(live, index) in lives"
                        :key="index"
                        src="https://yowin.fun/img/hpoint.7397a144.webp"
                        alt=""
                    />
                </p>
                <p class="hpPoint" v-else>Bạn đã hết lượt quay rồi</p>
            </div>
            <div class="wheel-container">
                <div class="row">
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
            </div>
            <the-sticky-row />
        </div>
    </div>
</template>

<script>
/* eslint-disable */
import TheStickyRow from "@/components/TheStickyRow.vue";
import "sweetalert2/dist/sweetalert2.min.css";
import axios from "axios";
export default {
    name: "HomeView",
    components: { TheStickyRow },
    created() {
        /*Fetch API*/
        // axios.get("https://localhost:7135/api/Home").then((response) => {
        //     this.prizeListOrigin = response.data;
        //     var prize0 = this.prizeListOrigin[0];
        //     var lastprize =
        //         this.prizeListOrigin[this.prizeListOrigin.length - 1];
        //     this.prizeListOrigin.forEach((element) => {
        //         if (element.name != "P.Codes") {
        //             this.chosenPrizeList.push(prize0);
        //             this.chosenPrizeList.push(element);
        //         } else if (
        //             element.name == lastprize.name &&
        //             element == "P.Codes"
        //         )
        //             this.chosenPrizeList.push(element);
        //     });
        // });
        var prize0 = this.prizeListOrigin[0];
        var lastprize = this.prizeListOrigin[this.prizeListOrigin.length - 1];
        this.prizeListOrigin.forEach((element) => {
            if (element.name != "P.Codes") {
                this.chosenPrizeList.push(prize0);
                this.chosenPrizeList.push(element);
            } else if (element.name == lastprize.name && element == "P.Codes")
                this.chosenPrizeList.push(element);
        });
        console.log(this.chosenPrizeList);
    },
    methods: {
         Onrolling() {
            if (this.lives > 0) {
                if (this.rolling) return;
                else {
                    const result = Math.random() * 100;
                    this.roll(result)
                    this.lives--;
                    // axios
                    //     .get("https://localhost:7135/api/Home/yourprize")
                    //     .then((result) => {
                    //         console.log(result.data)
                    //         this.roll(result.data);
                    //     });
                }
            } else this.$swal("Bạn đã hết lượt quay rồi");
        },
        roll(result) {
            var tempList = this.prizeListOrigin.sort((a, b) => {
                return a.percent - b.percent;
            });
            var position = 0;
            var array = [];
            for (var x = 0; x < this.chosenPrizeList.length; x++) {
                if (this.chosenPrizeList[x].name == result.name) {
                    array.push(x);
                }
            }
            console.log(array.length)
            position = array[Math.floor(Math.random() * array.length)];
            // this.wheelDeg =
            //     this.wheelDeg -
            //     (this.wheelDeg % 360) +
            //     6 * 360 +
            //     (360 / this.chosenPrizeList.length) * position;
            
            var currentPercent = 0;
            var i = 0;
            while (true) {
                if (result < tempList[i].percent + currentPercent) {
                    var array = [];
                    for (var x = 0; x < this.chosenPrizeList.length; x++) {
                        if (this.chosenPrizeList[x].name == tempList[i].name) {
                            array.push(x);
                        }
                    }
                    console.log(array);
                    position = array[Math.floor(Math.random() * array.length)];
                    this.wheelDeg =
                        this.wheelDeg -
                        (this.wheelDeg % 360) +
                        6 * 360 +
                        (360 / this.chosenPrizeList.length) * position;
                    break;
                } else {
                    currentPercent += tempList[i].percent;
                    i++;
                }
            }
            console.log(position);
            this.rolling = true;
            setTimeout(() => {
                this.rolling = false;

                this.$swal(
                    "Bạn đã nhận được " + this.chosenPrizeList[position].name
                );
                this.prizeHistory.push(this.chosenPrizeList[position]);
            }, 4500);
        },
    },
    data() {
        return {
            freeze: false,
            rolling: false,
            chosenPrizeList: [],
            wheelDeg: 0,
            lives: 3,
            prizeHistory: [],
            prizeListOrigin: [
                {
                    name: "P.Codes",
                    percent: 50,
                },
                {
                    name: "20$",
                    percent: 0.05,
                },
                {
                    name: "XiaoMi",
                    percent: 0.15,
                },
                {
                    name: "SJC",
                    percent: 3,
                },
                {
                    name: "SamSung Note 20",
                    percent: 1,
                },
                {
                    name: "10$",
                    percent: 0.5,
                },
                {
                    name: "5$",
                    percent: 0.3,
                },
                {
                    name: "2$",
                    percent: 5,
                },
                {
                    name: "1$",
                    percent: 15,
                },
                {
                    name: "0.5$",
                    percent: 20,
                },
            ],
        };
    },
};
</script>
<style scoped>
@import url("@/assets/css/body.css");
</style>
