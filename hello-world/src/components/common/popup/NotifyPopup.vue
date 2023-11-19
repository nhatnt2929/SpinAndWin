<!-- Popup.vue -->
<template>
    <div v-if="isOpen" class="popup">
        <div class="popup-content">
            <template v-if="isWin">
                <img class="image-win" src="@/public/images/win.png" />

                <h2>Congratulations</h2>
                <p>
                    <span>You have won...</span>
                    Try out our spin and win game to win one of our exciting prizes
                </p>
            </template>
            <template v-else>
                <img class="image-lose" src="@/public/images/lose.png" />
                <h2>Oh no</h2>
                <p>
                    <span>Try again...</span>
                    Try out our spin and win game to win one of our exciting prizes
                </p>
            </template>
            <button class="button-main" @click="closePopup">Try Again</button>
        </div>
        <div class="popup-backdrop" @click="closePopup"></div>
    </div>
</template>
  
<script>
export default {
    props: {
        title: {
            type: String,
        },
        subContent: {
            type: String,
        },
        content: {
            type: String,
        },
        isWin: {
            type: Boolean,
            default: true
        },
        isOpen: {
            type: Boolean
        }
    },
    created() {
        console.log("isOpen")
    },
    methods: {
        closePopup() {
            this.$emit("close-popup")
        },
    },
};
</script>
  
<style scoped lang="scss">
@import "@/public/scss/components/common/NotifyPopup.scss";
</style>
  