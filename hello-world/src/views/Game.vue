<template>
    <div class="container">
        <div class="header">
            <div class="header--icon-nav">
                <img src="@/public/images/nav.png"/>
            </div>
            <p class="header--title">Spin & Win</p>
            <div class="header--icon-notify" @click="mute">
                <img src="@/public/images/mute.png" v-if="isMute"/>
                <img src="@/public/images/speaker.png" v-else/>
            </div>
        </div>
        <div class="note">
            <p>
                <span>Feeling lucky?</span>
                Try out our spin and win game to win one of our exciting prizes.
            </p>
        </div>
        <audio style="display: none;" ref="audioPlayer" :src="audioSource" controls loop></audio>
        <WheelSpinner @play-music="playMusic"/>
        <LeaderBoard />
    </div>
</template>
<script>
import WheelSpinner from '@/components/WheelSpinner.vue';
import LeaderBoard from '@/components/LeaderBoard.vue';
export default {
    data() {
        return {
            isMute: false,
            audioSource: require("@/public/music/music.mp3"),
        }
    },
    components: {
        WheelSpinner,
        LeaderBoard
    },
    mounted() {
        this.playMusic()
    },
    methods: {
        mute() {
            this.isMute = !this.isMute
            this.$refs.audioPlayer.muted = this.isMute
        },
        playMusic(isPlay) {
            if (isPlay) {
                this.$refs.audioPlayer.play();
            } else {
                this.$refs.audioPlayer.pause();
            }
        },
    }
}
</script>
<style lang="scss">
@import "@/public/scss/Game.scss";
</style>