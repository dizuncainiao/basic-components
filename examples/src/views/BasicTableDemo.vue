<template>
  <div class="table-wrapper">
    <BasicTable
      ref="basicTable"
      :dataSource="fieldValue"
      :column-num="4"
      :columns="tableConfig"
    >
      <template #test="{ text }">
        <button>{{ text }}</button>
      </template>
    </BasicTable>
    <br />
    <hr />
    <br />
    <BasicTable
      ref="basicTable2"
      :dataSource="fieldValue"
      :column-num="2"
      :columns="tableConfig2"
    >
      <template #test="{ text }">
        <button>{{ text }}</button>
      </template>
    </BasicTable>
    <br />
    <hr />
    <br />
    <BasicTable
      ref="basicTable3"
      :dataSource="fieldValue"
      :column-num="6"
      :columns="tableConfig3"
    >
      <template #test="{ text }">
        <button>{{ text }}</button>
      </template>
    </BasicTable>
  </div>
</template>

<script setup lang="ts">
import { BasicTable } from "basic-components";
import { ref } from "vue";

// 1.后端返回的数据
const fieldValue = ref({
  calledName: "小江",
  calledNumber: "18156224704",
  callName: "小赵",
  callNumber: "18156228888",
  type: "外呼",
});

// 2.表格的渲染配置
const tableConfig = [
  {
    // 对应后端返回数据字段名
    dataIndex: "calledName",
    // 对应后端返回数据字段的名称，表格的列名
    name: "被叫姓名",
    // 合并列
    colspan: 3,
    // 需要进行特殊渲染的插槽名
    slotName: "test",
  },
  {
    dataIndex: "calledNumber",
    name: "被叫号码",
  },
  {
    dataIndex: "callName",
    name: "主叫姓名",
  },
  {
    dataIndex: "callNumber",
    name: "主叫号码",
  },
  {
    dataIndex: "type",
    name: "类型",
  },
];

const tableConfig2 = [
  {
    dataIndex: "calledName",
    name: "被叫姓名",
  },
  {
    dataIndex: "calledNumber",
    name: "被叫号码",
  },
  {
    dataIndex: "callName",
    name: "主叫姓名",
  },
  {
    dataIndex: "callNumber",
    name: "主叫号码",
  },
  {
    dataIndex: "type",
    name: "类型",
    slotName: "test",
  },
];

const tableConfig3 = [
  {
    dataIndex: "calledName",
    name: "被叫姓名",
  },
  {
    dataIndex: "calledNumber",
    name: "被叫号码",
  },
  {
    dataIndex: "callName",
    name: "主叫姓名",
  },
  {
    dataIndex: "callNumber",
    name: "主叫号码",
    colspan: 5,
  },
  {
    dataIndex: "type",
    name: "类型",
    slotName: "test",
    colspan: 5,
  },
];
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
