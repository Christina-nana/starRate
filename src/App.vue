<script lang="ts" setup>
  import Rate from './components/Rate.vue';
  import {ref} from 'vue'
  let score1 = ref<number>(3)
  let score2 = ref<number>(1)
</script>

<template>
  <Rate v-model = "score1" color="red">评分：</Rate>
  <Rate v-model = "score2" color="blue">打分：</Rate>
</template>

<style>
</style>
