<template>
    <div class="sprinner-container">
        <div class="wheel-container" :style="{ transform: `rotate(${rotation}deg)` }">
            <div v-for="(segment, index) in  segments " :key="index" class="wheel-segment"
                :style="{ backgroundColor: segment.color, transform: `rotate(${index * (360 / segments.length) + 20}deg)` }">
                <p class="segment-text" :style="{ transform: `rotate(${-25}deg)` }">
                    {{ segment.prize }}
                    
                </p>
                
                <img v-if="segment.image" class="segment-icon" :class="{ 'custom': segment.prize == '' }"
                    :src="segment.image" />
            </div>
        </div>
        <div class="play-button-container">
            <button @click="spin" :disabled="spinning" class="spin-button">
                <img src="@/public/images/play.png" />
            </button>
        </div>
        <div class="hook">
            <img :src="hook" />
        </div>
        <img src="@/public/images/border.png" class="overlay" />
        <NotifyComponent :isWin="indexPrizeWinArr.includes(result)" :isOpen="isOpenPopup" @close-popup="handleClosePopup" />
    </div>
</template>
  
<script>
import NotifyComponent from './common/popup/NotifyPopup.vue';
export default {
    components: { NotifyComponent },
    data() {
        return {
            hook: require("@/public/images/union.png"),
            segments: [
                { prize: "Prize one", color: "#BC48A8", image: require("@/public/images/wheel-icon/crown.png") },
                { prize: "Prize one", color: "#BC2504", image: null },
                { prize: "", color: "#EF5716", image: require("@/public/images/wheel-icon/question.png") },
                { prize: "Prize one", color: "#F1BB1C", image: null },
                { prize: "Prize one", color: "#F3D147", image: require("@/public/images/wheel-icon/gift.png") },
                { prize: "Prize one", color: "#A9C711", image: require("@/public/images/wheel-icon/money.png") },
                { prize: "Prize one", color: "#32A7C4", image: null },
                // { prize: "Prize one", color: "#8670B7", image: null },
                { prize: "Prize one", color: "#7A49CF", image: require("@/public/images/wheel-icon/coin.png") },
                { prize: "", color: "#8236BE", image: require("@/public/images/wheel-icon/sad.png") },
            ],
            spinning: false,
            isOpenPopup: false,
            rotation: 0,
            result: null,
            spinsLeft: 3,
            indexPrizeWinArr: [0, 4, 5, 7],
        };
    },
    methods: {
        spin() {
            if (this.spinsLeft > 0 && !this.spinning) {
                this.$emit('play-music', true)
                this.spinning = true;

                const baseRotation = this.rotation;
                const spinDuration = 5000;
                const numberOfSegments = this.segments.length;
                const segmentAngle = 360 / numberOfSegments;
                const randomTargetSegment = Math.floor(Math.random() * numberOfSegments);
                const targetRotation = baseRotation + (randomTargetSegment * segmentAngle);

                const startTime = performance.now();
                
                const animateSpin = (timestamp) => {
                    const progress = (timestamp - startTime) / spinDuration;
                    const easedProgress = 1 - Math.pow(1 - progress, 2);
                    this.rotation = baseRotation + easedProgress * (targetRotation - baseRotation) * 50;
                    if (progress < 1) {
                        requestAnimationFrame(animateSpin);
                    } else {
                        this.rotation = (this.rotation + 360) % 360;
                        const degreesPerSegment = 360 / numberOfSegments;
                        const indexTmp = Math.floor(this.rotation / degreesPerSegment)
                        const index = numberOfSegments - (indexTmp + 1)
                        this.result = index;
                        this.spinning = false;
                        this.isOpenPopup = true;
                        this.$emit('play-music', false);
                    }
                };
                
                requestAnimationFrame(animateSpin);
                this.spinsLeft -= 1;
                }
            
        },
        handleClosePopup() {
            this.isOpenPopup = false;
        }
    },
};
</script>
  
<style lang="scss">
@import "@/public/scss/components/WheelSpinner.scss";
</style>
  

