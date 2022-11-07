<template>
  <BasicLine :data="data" />
</template>

<script lang="ts" setup>
import { BasicLine } from "basic-components";
import { ref } from "vue";

const data = ref([
  {
    title: "呼叫成功",
    value: 60,
    color: "blue",
  },
  {
    title: "呼叫失败",
    value: 25,
    color: "red",
  },
  {
    title: "未执行",
    value: 15,
    color: "lightgray",
  },
]);
</script>

<script lang="ts">
export default {
  name: "BasicLineDemo",
};
</script>

<style scoped lang="less"></style>
