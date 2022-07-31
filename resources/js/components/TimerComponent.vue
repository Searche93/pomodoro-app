<template>
    <div class="mb-8" v-if="msg">
        <p class="text-4xl p-6 bg-gray-200 dark:bg-gray-800 text-center rounded">
            Timer stopped! :)
        </p>
    </div>

    <div class="text-center mb-8">
        <p class="text-8xl">
            <span class="-mr-2">
                <span class="-mr-4" v-if="this.timerMinutes < 10">0</span>
                {{ timerMinutes }}
            </span>
            :
            <span class="-ml-2">
                <span class="-mr-4" v-if="this.timerSeconds < 10">0</span>
                {{ timerSeconds }}
            </span>
        </p>
    </div>

    <div class="mt-8">
        <p>
            <button @click="startTimer()"
                    v-bind:disabled="isRunning"
                    class="mr-4 bg-blue-700 rounded-lg p-3 hover:bg-blue-500 transition-all ease-in-out text-white">
                Start the timer!
            </button>

            <button @click="pauseTimer()"
                    class="mr-4 bg-green-700 rounded-lg p-3 hover:bg-green-500 transition-all ease-in-out text-white">
                Pause the timer!
            </button>

            <button @click="stopTimer()"
                    class="mr-4 bg-red-700 rounded-lg p-3 hover:bg-red-500 transition-all ease-in-out text-white">
                Stop the timer!
            </button>
        </p>
    </div>
</template>

<script>
// TODO: Tijd opslaan in localstorage

export default {
    name: "TimerComponent",
    data() {
        return {
            msg: false,
            isRunning: false,
            timerMinutes: 15,
            timerSeconds: 0,
            secondsReset: 59,
        }
    },
    methods: {
        countdown() {
            const timer = setInterval(() => {
                if(this.isRunning) {
                    if (this.timerMinutes === 0 && this.timerSeconds === 0) {
                        this.stopTimer()
                    }
                    this.timerSeconds--;
                    if (this.timerSeconds < 0) {
                        this.timerSeconds = this.secondsReset;
                        this.timerMinutes--;
                    }
                } else {
                    clearInterval(timer);
                }
            }, 1000);
        },
        resetTimer() {
          this.timerMinutes = 15;
          this.timerSeconds = 0;
        },
        startTimer() {
            this.msg = false;
            this.isRunning = true;
            this.countdown();
        },
        stopTimer() {
            this.isRunning = false;
            this.msg = true;
            this.resetTimer();
        },
        pauseTimer(){
            this.isRunning = false;
        },
    },
}
</script>

<style scoped>

</style>
