<template>
  <div class="table-wrapper">
    <BasicTable ref="basicTable" :data="tableData">
      <template #test="{ text }">
        <button type="primary">{{ text }}</button>
      </template>
    </BasicTable>
    <br />
    <hr />
    <br />
    <BasicTable ref="basicTable2" :data="tableData2">
      <template #test="{ text }">
        <button type="primary">{{ text }}</button>
      </template>
    </BasicTable>
    <br />
    <hr />
    <br />
    <BasicTable ref="basicTable3" :data="tableData3">
      <template #test="{ text }">
        <button type="primary">{{ text }}</button>
      </template>
    </BasicTable>
  </div>
</template>

<script setup lang="ts">
import { BasicTable } from "basic-components";

import { onMounted, ref, unref } from "vue";

const basicTable = ref();
const basicTable2 = ref();
const basicTable3 = ref();

// 1.后端返回的数据
const fieldValue = {
  calledName: "小江",
  calledNumber: "18156224704",
  callName: "小赵",
  callNumber: "18156228888",
  type: "外呼",
};

// 2.表格的渲染配置
const tableConfig = [
  {
    // 对应后端返回数据字段的 key
    key: "calledName",
    // 对应后端返回数据字段的名称，表格的列名
    name: "被叫姓名",
    // 合并列
    colspan: 3,
    // 需要进行特殊渲染的插槽名
    slotName: "test",
  },
  {
    key: "calledNumber",
    name: "被叫号码",
  },
  {
    key: "callName",
    name: "主叫姓名",
  },
  {
    key: "callNumber",
    name: "主叫号码",
  },
  {
    key: "type",
    name: "类型",
  },
];

const tableConfig2 = [
  {
    key: "calledName",
    name: "被叫姓名",
  },
  {
    key: "calledNumber",
    name: "被叫号码",
  },
  {
    key: "callName",
    name: "主叫姓名",
  },
  {
    key: "callNumber",
    name: "主叫号码",
  },
  {
    key: "type",
    name: "类型",
    slotName: "test",
  },
];

const tableConfig3 = [
  {
    key: "calledName",
    name: "被叫姓名",
  },
  {
    key: "calledNumber",
    name: "被叫号码",
  },
  {
    key: "callName",
    name: "主叫姓名",
  },
  {
    key: "callNumber",
    name: "主叫号码",
    colspan: 5,
  },
  {
    key: "type",
    name: "类型",
    slotName: "test",
    colspan: 5,
  },
];

const tableData = ref([]);
const tableData2 = ref([]);
const tableData3 = ref([]);

onMounted(() => {
  // 3.生成表格数据
  tableData.value = unref(basicTable).getTableData(fieldValue, tableConfig, 4);
  tableData2.value = unref(basicTable).getTableData(
    fieldValue,
    tableConfig2,
    2
  );
  tableData3.value = unref(basicTable).getTableData(
    fieldValue,
    tableConfig3,
    6
  );
});
</script>

<script lang="ts">
export default {
  name: "BasicTableDemo",
};
</script>

<style scoped lang="less">
.table-wrapper {
  background: #fff;
  padding: 20px;
}
</style>
