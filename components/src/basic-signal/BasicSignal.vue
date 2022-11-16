<template>
  <div class="basic-signal">
    <span
      class="signal-item"
      :style="{ '--signalColor': signalColor[0] }"
    ></span>
    <span
      class="signal-item"
      :style="{ '--signalColor': signalColor[1] }"
    ></span>
    <span
      class="signal-item"
      :style="{ '--signalColor': signalColor[2] }"
    ></span>
  </div>
</template>

<script lang="ts" setup>
import { computed, onBeforeUnmount, onMounted, ref, unref } from "vue";

const signalColors = {
  offline: ["red", "red", "red"],
  excellent: ["green", "green", "green"],
  good: ["green", "green"],
  commonly: ["green"],
  bad: ["red", "red"],
};

// navigator.connection.rtt（0 offline、50 no throttling、600 fast 3g、2100 slow 3g）
const rtt = ref(0);
const timer = ref();

const signalColor = computed(() => {
  const { offline, excellent, good, commonly, bad } = signalColors;
  // 离线
  if (unref(rtt) === 0) {
    return offline;
  } else if (unref(rtt) > 0 && unref(rtt) <= 300) {
    return excellent;
  } else if (unref(rtt) > 300 && unref(rtt) <= 700) {
    return good;
  } else if (unref(rtt) > 700 && unref(rtt) <= 2200) {
    return commonly;
  }
  return bad;
});

onMounted(() => {
  const c = navigator.connection as any;
  rtt.value = c.rtt;

  timer.value = setInterval(() => {
    rtt.value = c.rtt;
  }, 2000);
});

onBeforeUnmount(() => {
  clearInterval(timer.value);
});
</script>

<script lang="ts">
export default {
  name: "BasicSignal",
};
</script>

<style scoped lang="less">
.basic-signal {
  width: 10px;
  height: 10px;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  /*todo css 变量作用域讲解*/
  //--signalColor: gray;

  .signal-item {
    width: 2px;
    /*todo css 变量默认值讲解*/
    background: var(--signalColor, gray);
    transition: ease-in;

    &:nth-child(1) {
      height: 5px;
    }

    &:nth-child(2) {
      height: 7px;
    }

    &:nth-child(3) {
      height: 10px;
    }
  }
}
</style>
