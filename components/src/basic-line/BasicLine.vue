<template>
  <div class="basic-line">
    <div class="line">
      <span
        v-for="(item, index) of lineData"
        :key="index"
        :style="{
          background: item.color,
          width: item.width,
        }"
      ></span>
    </div>
    <div class="legend">
      <span
        v-for="(item, index) of lineData"
        :key="index"
        :style="{
          '--bgColor': item.color,
        }"
      >
        {{ item.title }}
      </span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { computed } from "vue";

type Item = {
  title: string;
  value: number;
  color: string;
  width?: string;
};

const props = defineProps<{
  data: Item[];
}>();

const lineData = computed(() => {
  const total = props.data.map((item) => item.value).reduce((a, b) => a + b);
  return props.data.map((item) => {
    return {
      ...item,
      width: `${(item.value / total) * 100}%`,
    };
  });
});
</script>

<script lang="ts">
export default {
  name: "BasicLine",
};
</script>

<style scoped lang="less">
.basic-line {
  width: 100%;
  line-height: 1;

  .line {
    display: flex;
    height: 10px;
    border-radius: 10px;
    overflow: hidden;

    > span {
      height: 100%;
      transition: 0.3s ease-in;
    }
  }

  .legend {
    margin-top: 15px;
    display: flex;
    justify-content: center;
    gap: 40px;
    font-size: 12px;

    > span {
      display: inline-flex;
      align-items: center;
      gap: 6px;

      &::before {
        display: inline-block;
        width: 8px;
        height: 8px;
        border-radius: 8px;
        content: "";
        background-color: var(--bgColor);
      }
    }
  }
}
</style>
