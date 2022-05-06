<template>
    <div class="wrapper">
        <div class="spin">
            <div class="row">
                <h3>☆Lucky Wheel☆</h3>
            </div>
            <div class="row">
                <p class="hpPoint"
                 v-if="lives > 0"
                >
                    <img
                       
                        v-for="(live,index) in lives"
                        :key="index"
                        src="https://yowin.fun/img/hpoint.7397a144.webp"
                        alt=""
                    />
                </p>
                <p class="hpPoint"
                v-else
                >
                  Bạn đã hết lượt quay rồi
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
import 'sweetalert2/dist/sweetalert2.min.css';
import axios from 'axios'
export default {
    name: "HomeView",
    components: { TheStickyRow },
     created() {
            axios.get('https://localhost:7135/api/Home')
            .then((response)=>{
              this.prizeListOrigin = response.data
                var prize0 = this.prizeListOrigin[0]
                var lastprize = this.prizeListOrigin[this.prizeListOrigin.length - 1]
           this.prizeListOrigin.forEach(element => {            
              if(element.name != "P.Codes") {
                 this.chosenPrizeList.push(prize0)
                this.chosenPrizeList.push(element)
              }else if(element.name == lastprize.name && element == "P.Codes") this.chosenPrizeList.push(element)
              
           });
            })
        },
    methods: {
        Onrolling() {
          if(this.lives > 0){
                if (this.rolling) return;
            else{
                 const result = Math.floor(
                Math.random() * this.chosenPrizeList.length
            );
            this.lives --
            this.roll(result);
            }
          }
          else this.$swal('Bạn đã hết lượt quay rồi');
        },
        roll(result) {
            
            this.rolling = true;
            this.rol = (this.wheelDeg % 360) +6 * 360 +(360 / this.chosenPrizeList.length) * result
            this.wheelDeg =this.wheelDeg - (this.wheelDeg % 360) +6 * 360 +(360 / this.chosenPrizeList.length) * result;
            setTimeout(() => {
                this.rolling = false;
                this.$swal("Bạn đã nhận được " + this.chosenPrizeList[result].name)
                this.prizeHistory.push(this.chosenPrizeList[result])
            }, 4500);
        },
    },
    data() {
        return {
            freeze: false,
            rolling: false,
            chosenPrizeList:[],
            rol:0,
            wheelDeg: 0,
            lives:3,
            prizeHistory:[],
            prizeListOrigin: [
                // {
                //    name: "P.Code",
                //      percent: 20/360*100,
                // },
                // {
                //     name: "20$",
                //     percent: 20/360*100,
                // },
                // {
                //     name: "P.Code",
                //      percent: 20/360*100,
                // },
                // {
                //     name: "XiaoMi",
                //      percent: 20/360*100,
                // },
                // {
                //     name: "P.Code",
                //       percent: 20/360*100,
                // },
                // {
                //     name: "SJC",
                //      percent: 20/360*100,
                // },
                // {
                //     name: "P.Code",
                //       percent: 20/360*100,
                // },
                //   {
                //     name: "SamSung Note 20",
                //       percent: 20/360*100,
                // },
                //   {
                //     name: "P.Code",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "10$",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "P.Codes",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "5$",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "P.Code",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "2$",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "P.Code",
                //       percent: 20/360*100,
                // },
                //   {
                //     name: "1$",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "P.Code",
                //      percent: 20/360*100,
                // },
                //   {
                //     name: "5$",
                //     percent: 20/360*100,
                // },
            ],
        };
    },
};
</script>
<style scoped>
@import url("@/assets/css/body.css");
</style>
