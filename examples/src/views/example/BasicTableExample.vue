<template>
  <table class="basic-table">
    <tbody>
      <tr>
        <td class="th">姓名</td>
        <td>张三</td>
        <td class="th">年龄</td>
        <td>20</td>
      </tr>
      <tr>
        <td class="th">姓名</td>
        <td colspan="3">张三</td>
      </tr>
    </tbody>
  </table>
</template>

<script lang="ts" setup>
const tableData = [
  [
    {
      isTh: true,
      value: "姓名",
    },
    {
      isTh: false,
      value: "张三",
    },
    {
      isTh: true,
      value: "年龄",
    },
    {
      isTh: false,
      value: "20",
    },
  ],
  [
    {
      isTh: true,
      value: "姓名",
    },
    {
      isTh: false,
      value: "张三",
      colspan: 3,
    },
  ],
];
</script>

<script lang="ts">
export default {
  name: "BasicTableExample",
};
</script>

<style scoped lang="less">
.basic-table {
  width: 100%;
  margin-bottom: 50px;
  border-collapse: collapse;
  border: 1px solid #edf1f6;
}

td {
  border: 1px solid #edf1f6;
  padding-left: 24px;
  padding-right: 24px;
  height: 60px;
  color: #242934;
}

td.th {
  background: rgb(249, 250, 253);
  color: #646b7a;
}
</style>
