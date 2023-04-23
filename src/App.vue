<template>
    <div class="container">
        <MainScreen v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart($event)"/>
        <InteractScreen 
            v-if="statusMatch === 'match'" 
            :cardsContext="settings.cardsContext"
            @onFinished="onGetResult()"
        />
        <ResultScreen 
            v-if="statusMatch === 'result'"
            :timer="timer"
            @startAgain="statusMatch = 'default'"
        />
        <Copyright />
        
    </div>
</template>
<script>
import MainScreen from './components/MainScreen.vue';
import InteractScreen from './components/InteractScreen.vue';
import ResultScreen from './components/ResultScreen.vue';
import Copyright from './components/Copyright.vue';
import { shuffled } from './utils/array.js'

    export default {
        components: {
            MainScreen,
            InteractScreen,
            ResultScreen,
            Copyright
        },
        data() {
            return {
                settings: {
                    totalOfCards: 0,
                    cardsContext: [],
                    timerCount: null,
                },
                statusMatch: "default",
                timer: 0
            }
        },
        methods: {
            onHandleBeforeStart(config) {
                console.log(config);
                this.settings.totalOfCards = config.totalOfCards
                const firstCards = Array.from(
                    { length: this.settings.totalOfCards / 2}, 
                    (_,i) => i+1
                );
                const secondCards = [...firstCards]
                const cards = [...firstCards, ...secondCards]
                this.settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))))
                this.settings.timerCount = new Date().getTime();

                this.statusMatch = "match"
            },
            onGetResult() {
                this.timer = new Date().getTime() - this.settings.timerCount
                this.statusMatch = 'result'
            }
        }
    }
</script>
<style>
    
</style>
