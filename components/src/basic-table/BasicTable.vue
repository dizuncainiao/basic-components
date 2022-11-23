<template>
  <table class="basic-table">
    <tbody>
      <tr v-for="(tds, index) of tableData" :key="index">
        <td
          v-for="(td, subIndex) of tds"
          :key="subIndex"
          :colspan="td.colspan"
          :class="td.isTh && 'th'"
        >
          <!--优先级：插槽 >  text-->
          <slot v-if="td.slotName" :name="td.slotName" :text="td.text"></slot>
          <template v-else>{{ td.text }}</template>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import { computed } from "vue";

type Td = {
  isTh: boolean; // 是否是表格标题
  text: string; // 列内容
  colspan?: number; // 合并列
  slotName?: string; // 插槽名
};

type Tr = Td[];

type TableData = Tr[];

type DataSource = Record<string, any>;

type Column = {
  dataIndex: string; // 对应后端返回数据字段名
  name: string; // 对应后端返回数据字段的名称含义，表格的列名
  colspan?: number; // 合并列
  slotName?: string; // 需要进行特殊渲染的插槽名
};

type Columns = Column[];

const props = defineProps<{
  dataSource: DataSource; // 数据源
  columns: Columns; // 列配置
  columnNum: number; // 表格列数
}>();

function getBasicData(dataSource: DataSource, columns: Columns) {
  console.log(dataSource, columns);
  const list: Td[] = [];
  columns.forEach((item) => {
    // th数据
    const th = {
      isTh: true,
      colspan: 1,
      text: item.name,
    };
    // td数据
    const td = {
      isTh: false,
      colspan: item.colspan || 1,
      text: dataSource[item.dataIndex],
      slotName: item.slotName,
    };

    list.push(th, td);
  });

  return list;
}

function handleBasicData(target: Td[], colNum: number, tableData: TableData) {
  let sum = 0;
  let i = 0;
  let item = [];

  while (target[i]?.colspan) {
    sum += target[i].colspan!;
    item.push(target[i]);
    if (sum === colNum) {
      tableData.push(item);
      sum = 0;
      item = [];
    }
    i++;
  }
}

const tableData = computed(() => {
  const result: TableData = [];
  const basicData = getBasicData(props.dataSource, props.columns);
  handleBasicData(basicData, props.columnNum, result);
  return result;
});
</script>

<script lang="ts">
export default {
  name: "BasicTable",
};
</script>

<style scoped lang="less">
.basic-table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid #edf1f6;

  td {
    border: 1px solid #edf1f6;
    //border-bottom: 1px solid #edf1f6;
    //border-right: 1px solid #edf1f6;
    padding-left: 24px;
    padding-right: 24px;
    height: 60px;
    color: #242934;

    &.th {
      background: rgb(249, 250, 253);
      color: #646b7a;
    }
  }
}
</style>
