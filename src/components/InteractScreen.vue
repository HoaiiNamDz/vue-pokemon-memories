<template lang="">
    <div class="screen">
        <div class="screen__inner"
            :style="{
                width: `${((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 + 16)* Math.sqrt(cardsContext.length)}px`
            }"
        >
            <card
                v-for="(card, index) in cardsContext" 
                :key="index" 
                :ref="`card-${index}`"
                :imgBackFaceUrl="`images/${card}.png`"
                :card="{ index, value: card}"
                @onFlip="checkRules($event)"
                :cardsContext="cardsContext"
            />
        </div>
    </div>
</template>
<script>
import Card from './Card.vue'
export default {
    props: {
        cardsContext: {
            type: Array,
            default: function() {
                return []
            }
        }
    },
    data() {
        return {
            rules: []
        }
    },
    components: {
        Card
    },
    methods: {
        checkRules(card) {
            if(this.rules.length === 2) {
                return false
            }
            this.rules.push(card)
            if(this.rules[0].index != this.rules[1].index) {
                if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value ) {
                    console.log('right');
                    this.$refs[`card-${this.rules[0].index}`][0].onDisabledMode();
                    this.$refs[`card-${this.rules[1].index}`][0].onDisabledMode();
                    this.rules = []

                    const disabledElements = document.querySelectorAll('.screen .card.disabled')
                    if(disabledElements && disabledElements.length === this.cardsContext.length - 2) {
                        setTimeout(() => {
                            this.$emit('onFinished')
                        }, 800)
                    }
                } else if(this.rules.length === 2 && this.rules[0].value !== this.rules[1].value) {
                    setTimeout(() => {
                        this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
                        this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
                        this.rules = []
                    },800)
                } else {
                    return false
                }
            } else {
                this.rules = []
            }
        }
    }
}
</script>
<style lang="css" scoped>
    .screen {
        text-align: center;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        background-color: var(--dark);
        color: var(--light);
        z-index: 2;
    }
    .screen__inner {
        display: flex;
        flex-wrap: wrap;
        margin: 2rem auto;
    }
</style>