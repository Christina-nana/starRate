<script lang="ts" setup>
import { ref, computed } from 'vue'
interface StyleWidth {
    width: string
}

let props = defineProps<{
    modelValue: number,
    color?:string
}>()

const emits = defineEmits(['update:modelValue'])

const score = ref(props.modelValue)

const starWidth = computed<StyleWidth>(() => {
    return { width: score.value + 'em' }
})

function mouseOver(num: number) {
    score.value = num
}

function mouseOut() {
    score.value = props.modelValue
}

function clickStar(num: number) {
    emits('update:modelValue', num)
}
</script>

<template>
    <div>
        <slot />
        <div class="rate" @mouseout="mouseOut" :style="{color}">
            <span @mouseover="mouseOver(num)" v-for="num in 5" :key="num" class="star">☆</span>
            <div class="solid" :style="starWidth">
                <span
                    @mouseover="mouseOver(num)"
                    @click="clickStar(num)"
                    v-for="num in 5"
                    :key="num"
                    class="star"
                >★</span>
            </div>
            {{ modelValue }}
        </div>
    </div>
</template>

<style>
.rate {
    display: inline-block;
    position: relative;
}
.solid {
    position: absolute;
    left: 0;
    top: 0;
    width: 0;
    overflow: hidden;
}
.star {
    cursor: pointer;
}
</style>