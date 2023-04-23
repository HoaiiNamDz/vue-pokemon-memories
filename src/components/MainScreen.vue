<template lang="">
    <div class="screen">
        <h1>POKE MEMORIES</h1>
        <h3>Select mode to start game</h3>
        <div class="actions">
            <button @click="onStart(16)">
                <span>4x4</span>
                <span>Easy</span>
            </button>
            <button @click="onStart(36)">
                <span>6x6</span>
                <span>Normal</span>
            </button>
            <button @click="onStart(64)">
                <span>8x8</span>
                <span>Hard</span>
            </button>
            <button @click="onStart(100)">
                <span>10x10</span>
                <span>Nightmare</span>
            </button>
        </div>
    </div>
</template>
<script>
export default {

    methods: {
        onStart(totalOfCards) {
            this.$emit('onStart', { totalOfCards })
        }
    }
}
</script>
<style lang="css" scoped>
    button {
        width: 150px;
        height: 150px;
        margin: 0 20px;
        border-radius: 8px;
        color: var(--light);
        background-color: var(--dark);
        border: 1px solid var(--light);
    }
    span {
        display: block;
    }
    .screen {
        width: 100%;
        height: 100vh;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 2;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        background-color: var(--dark);
        color: var(--light);
    }
    .screen h1 {
        font-size: 4.5rem;
        text-transform: uppercase;
    }
    .screen p {
        font-size: 2rem;
    }
    button:hover {
        background-color: var(--light);
        color: var(--dark);
    }
    button span:first-child {
        font-size: 2rem;
    }
    button span:last-child {
        display: block;
        font-size: 1.25rem;
        margin-top: 0.5rem;
    }
</style>