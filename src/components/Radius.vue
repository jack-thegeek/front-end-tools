<script setup>
import { ref } from 'vue'

const wheelColor = ref('#e6f5eb')
</script>

<template>
    <div class="container">
        <div class="stage">
            <div class="left"></div>
            <div class="right"></div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.container {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    margin: 0 auto;
    max-width: 1280px;
    padding: 100px 2rem 2rem;
    position: relative;
}

.stage {
    width: 100%;
    display: flex;
    gap: 40px;
}

.left,
.right {
    width: 50%;
    height: 420px;
    padding: 1rem;
    border-radius: 1rem;
    background-color: aliceblue;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, .1), 0 2px 4px -2px rgba(0, 0, 0, .1);
}

@media (max-width: 700px) {
    .stage {
        flex-direction: column;
    }

    .left,
    .right {
        width: 100%;
    }
}
</style>