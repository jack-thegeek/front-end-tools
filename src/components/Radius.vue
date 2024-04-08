<script setup>
import {computed, ref} from 'vue'

const outerR = ref(65)
const innerR = ref(30)
const padding = ref(`${outerR.value - innerR.value}`)

// 修改外圆角，保持内边距不变，自动修正内圆角
// 修改内边距，保持外圆角不变，自动修正内圆角
function fixInnerR() {
    let fix = Number(outerR.value) - Number(padding.value);
    innerR.value = 0 <= fix && fix <= 100 ? fix : 0;
}

// 修改内圆角，保持内边距不变，自动修正外圆角
function fixOuterR() {
    let fix = Number(innerR.value) + Number(padding.value);
    outerR.value = 0 <= fix && fix <= 100 ? fix : 100;
}

</script>

<template>
    <div class="container">
        <div class="stage">
            <div class="left">
                <div :style="{ borderRadius: `${outerR}px`, padding: `${padding}px` }" class="outer-box">
                    <div :style="{ borderRadius: `${innerR}px` }" class="inner-box"></div>
                </div>
            </div>
            <div class="right">
                <div class="space-between">
                    <div>外圆角</div>
                    <div>{{ outerR }}px</div>
                </div>
                <input type="range" :min="0" :max="100" v-model="outerR" @input="fixInnerR">

                <div class="space-between">
                    <div>内圆角</div>
                    <div>{{ innerR }}px</div>
                </div>
                <input type="range" :min="0" :max="100" v-model="innerR" @input="fixOuterR">

                <div class="space-between">
                    <div>内边距</div>
                    <div>{{ padding }}px</div>
                </div>
                <input type="range" :min="0" :max="100" v-model="padding" @input="fixInnerR">
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.outer-box {
    width: 60%;
    height: 60%;
    border: 3px solid #aec6e2;
}

.inner-box {
    width: 100%;
    height: 100%;
    background-color: #e4ebf5;
    border: 3px solid #cfddee;
}

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
    width: 90%;
    display: flex;
    gap: 40px;
}

.left,
.right {
    width: 50%;
    height: 420px;
    padding: 1rem;
    border-radius: 1rem;
    background-color: #fafafa;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, .1), 0 2px 4px -2px rgba(0, 0, 0, .1);
}

.left {
    display: flex;
    justify-content: center;
    align-items: center;
}

.right {
    padding: 4rem;

    input {
        width: 100%;
        display: block;
        margin-bottom: 2rem;
    }
}

.space-between {
    display: flex;
    justify-content: space-between;
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